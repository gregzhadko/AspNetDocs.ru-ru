---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: Общие сведения о представлениях MVC ASP.NET (VB) | Документация Майкрософт
author: StephenWalther
description: Что такое представление MVC ASP.NET и как оно отличается от HTML-страницы? В этом руководстве Стивен Вальтер знакомит вас с представлениями и демонстрирует, как можно выполнить t...
ms.author: riande
ms.date: 02/16/2008
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: a07d15cb14e9ef90b62c5a8702dee53f1a0a6032
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044671"
---
# <a name="aspnet-mvc-views-overview-vb"></a>Общие сведения о представлениях ASP.NET MVC (VB)

по [Стивен Вальтер](https://github.com/StephenWalther)

> Что такое представление MVC ASP.NET и как оно отличается от HTML-страницы? В этом руководстве Стивен Вальтер знакомит вас с представлениями и демонстрирует, как можно воспользоваться преимуществами представления данных и вспомогательных функций HTML в рамках представления.

Цель этого руководства — предоставить краткое введение в представления ASP.NET MVC, просмотр данных и вспомогательные методы HTML. К концу этого руководства вы узнаете, как создавать новые представления, передавать данные из контроллера в представление и использовать вспомогательные методы HTML для создания содержимого в представлении.

## <a name="understanding-views"></a>Основные сведения о представлениях

В отличие от страниц ASP.NET или Active Server, ASP.NET MVC не содержит ничего, непосредственно соответствующего странице. В приложении ASP.NET MVC отсутствует страница на диске, соответствующая пути URL-адреса, введенного в адресной строке браузера. Самым близким к странице в приложении ASP.NET MVC является то, что оно называется *представлением*.

В приложении ASP.NET MVC входящие запросы браузера сопоставляются с действиями контроллера. Действие контроллера может возвращать представление. Однако действие контроллера может выполнять другие действия, например перенаправление на другое действие контроллера.

В листинге 1 содержится простой контроллер с именем HomeController. HomeController предоставляет два действия контроллера с именами index () и Details ().

**Листинг 1-HomeController. vb**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

Вы можете вызвать первое действие, действие index (), введя следующий URL-адрес в адресную строку браузера:

/хоме/индекс

Вы можете вызвать второе действие, действие Details (), введя этот адрес в браузере:

/хоме/детаилс

Действие index () возвращает представление. Большинство создаваемых действий будут возвращать представления. Однако действие может возвращать другие типы результатов действий. Например, действие Details () возвращает Редиректтоактионресулт, который перенаправляет входящий запрос в действие index ().

Действие index () содержит следующую одну строку кода:

View ()

Эта строка кода возвращает представление, которое должно находиться по следующему пути на веб-сервере:

\виевс\хоме\индекс.аспкс

Путь к представлению выводится из имени контроллера и имени действия контроллера.

При желании вы можете быть явными для представления. Следующая строка кода возвращает представление с именем Fred:

Вид (Fred)

При выполнении этой строки кода представление возвращается по следующему пути:

\виевс\хоме\фред.аспкс

> [!NOTE] 
> 
> Если вы планируете создавать модульные тесты для приложения ASP.NET MVC, рекомендуется явно указывать имена представлений. Таким образом, можно создать модульный тест, чтобы убедиться, что ожидаемое представление было возвращено действием контроллера.

## <a name="adding-content-to-a-view"></a>Добавление содержимого в представление

Представление — это стандартный HTML-документ (X), который может содержать скрипты. Для добавления динамического содержимого в представление используются скрипты.

Например, представление в листинге 2 отображает текущую дату и время.

**Листинг 2. \Виевс\хоме\индекс.аспкс**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

Обратите внимание, что текст страницы HTML в листинге 2 содержит следующий скрипт:

&lt;% Response. Write (DateTime. Now)%&gt;

&lt; &gt; Для обозначения начала и конца скрипта используются разделители скриптов% и%. Этот сценарий написан на языке Visual Basic. Он отображает текущую дату и время, вызывая метод Response. Write () для отрисовки содержимого в браузере. Разделители скриптов &lt; % и% &gt; могут использоваться для выполнения одной или нескольких инструкций.

Так как вы вызываете Response. Write () так часто, корпорация Майкрософт предоставляет вам ярлык для вызова метода Response. Write (). Представление в листинге 3 использует разделители &lt; % = и% &gt; в качестве ярлыка для вызова Response. Write ().

**Листинг 3. Views\Home\Index2.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

Для создания динамического содержимого в представлении можно использовать любой язык .NET. Как правило, для записи контроллеров и представлений используется либо Visual Basic .NET, либо C#.

## <a name="using-html-helpers-to-generate-view-content"></a>Использование вспомогательных функций HTML для создания содержимого представления

Чтобы упростить добавление содержимого в представление, можно воспользоваться преимуществом, которое называется *вспомогательным модулем HTML*. HTML-вспомогательный метод, как правило, является методом, который создает строку. Вспомогательные элементы HTML можно использовать для создания стандартных HTML-элементов, таких как текстовые поля, ссылки, раскрывающиеся списки и списки.

Например, представление в листинге 4 использует преимущества трех вспомогательных функций HTML — Бегинформ (), TextBox () и Password () для создания формы входа (см. рис. 1).

**Листинг 4 — \Виевс\хоме\логин.аспкс**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]

[![Диалоговое окно New Project (Новый проект)](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)

**Рис. 01**. Стандартная форма входа ([щелкните, чтобы просмотреть изображение с полным размером](asp-net-mvc-views-overview-vb/_static/image2.png))

Все методы вспомогательных методов HTML вызываются в свойстве HTML представления. Например, можно отобразить текстовое поле, вызвав метод HTML. TextBox ().

Обратите внимание, что при &lt; &gt; вызове вспомогательных методов HTML. TextBox () и HTML. Password () используются разделители скриптов% = и%. Эти вспомогательные методы просто возвращают строку. Чтобы отобразить строку в браузере, необходимо вызвать метод Response. Write ().

Использование вспомогательных методов HTML является необязательным. Они упрощают жизнь, уменьшая объем кода HTML и скрипта, который необходимо написать. Представление в листинге 5 отображает ту же форму, что и представление в листинге 4 без использования вспомогательных функций HTML.

**Листинг 5. \Виевс\хоме\логин.аспкс**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

Вы также можете создать собственные вспомогательные методы HTML. Например, можно создать вспомогательный метод GridView (), который автоматически отображает набор записей базы данных в HTML-таблице. В этом разделе рассматривается **Создание настраиваемых**вспомогательных функций HTML.

## <a name="using-view-data-to-pass-data-to-a-view"></a>Использование представления данных для передачи данных в представление

Для передачи данных из контроллера в представление используются данные представления. Представьте себе данные представления, например пакет, отправляемый по почте. Все данные, передаваемые из контроллера в представление, должны отправляться с помощью этого пакета. Например, контроллер в листинге 6 добавляет сообщение для просмотра данных.

**Листинг 6-Продуктконтроллер. vb**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

Свойство ViewData контроллера представляет коллекцию пар имен и значений. В листинге 6 метод Index () добавляет элемент в коллекцию данных View с именем Message со значением Hello World!. Когда представление возвращается методом index (), данные представления передаются в представление автоматически.

Представление в листинге 7 извлекает сообщение из данных представления и готовит его к просмотру в браузере.

**Листинг 7. \Виевс\продукт\индекс.аспкс**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

Обратите внимание, что представление использует преимущества вспомогательного метода HTML HTML. Encoded () при подготовке сообщения. Вспомогательный метод HTML HTML. Encoded () кодирует специальные символы, такие как &lt; и, &gt; в символы, которые могут быть зашифрованы для просмотра на веб-странице. При отрисовке содержимого, отправляемого пользователем на веб-сайт, необходимо кодировать содержимое, чтобы предотвратить атаки путем внедрения кода JavaScript.

(Поскольку мы создали сообщение в Продуктконтроллер, нам не нужно кодировать сообщение. Однако рекомендуется всегда вызывать метод HTML. Encoded () при отображении содержимого, полученного из представления данных в представлении.)

В листинге 7 мы использовали преимущества представления данных для передачи простого строкового сообщения из контроллера в представление. Можно также использовать представление данных для передачи других типов данных, таких как коллекция записей базы данных, из контроллера в представление. Например, если нужно отобразить содержимое таблицы базы данных Products в представлении, то необходимо передать коллекцию записей базы данных в представлении данные.

Также имеется возможность передачи строго типизированных данных представления из контроллера в представление. Этот раздел рассматривается в учебнике **понимание данных и представлений строго типизированного представления**.

## <a name="summary"></a>Сводка

В этом руководстве предоставлены краткие сведения о ASP.NET представлениях MVC, просмотре данных и вспомогательных элементах HTML. В первом разделе вы узнали, как добавлять новые представления в проект. Вы узнали, что необходимо добавить представление в правую папку, чтобы вызвать его из определенного контроллера. Далее обсуждалась тема вспомогательных функций HTML. Вы узнали, как вспомогательные методы HTML позволяют легко создавать стандартное содержимое HTML. Наконец, вы узнали, как использовать преимущества представления данных для передачи данных из контроллера в представление.

> [!div class="step-by-step"]
> [Назад](passing-data-to-view-master-pages-cs.md)
> [Вперед](creating-custom-html-helpers-vb.md)
