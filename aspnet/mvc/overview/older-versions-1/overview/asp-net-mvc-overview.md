---
uid: mvc/overview/older-versions-1/overview/asp-net-mvc-overview
title: ASP.NET Обзор MVC (ru) Документы Майкрософт
author: rick-anderson
description: Узнайте о различиях между приложением mVC ASP.NET и приложениями ASP.NET Web Forms. Узнайте, как решить, когда создавать ASP.NET приложение MVC.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2dcb44a4-5cbf-4d62-b363-718104082d86
msc.legacyurl: /mvc/overview/older-versions-1/overview/asp-net-mvc-overview
msc.type: authoredcontent
ms.openlocfilehash: 84810f168faa2e79a65ff3fb75e3654828bdb58f
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541017"
---
# <a name="aspnet-mvc-overview"></a>Общие сведения об ASP.NET MVC

[корпорацией Майкрософт](https://github.com/microsoft)

> Узнайте о различиях между приложением mVC ASP.NET и приложениями ASP.NET Web Forms. Узнайте, как решить, когда создавать ASP.NET приложение MVC.

Схема архитектуры Model-View-Controller (MVC) разделяет приложение на три основных компонента: модель, представление и контроллер. Платформа ASP.NET MVC является альтернативой шаблону ASP.NET Web Forms для создания веб-приложений на основе MVC. Платформа ASP.NET MVC является легковесной платформой отображения с широкими возможностями тестирования и, подобно приложениям на основе веб-форм, интегрирована с существующими функциями ASP.NET, например с главными страницами и проверкой подлинности на основе членства. Платформа MVC определена в пространстве имен **System.Web.Mvc** и является фундаментальной, поддерживаемой частью пространства имен **System.Web.**   
  
MVC представляет собой стандартный шаблон разработки, знакомый многим специалистам. Некоторые типы веб-приложений имеют преимущества при создании на платформе MVC. Для других может быть целесообразно использование традиционной схемы приложения ASP.NET, основанной на веб-формах и обратной передаче. В некоторых случаях возможно сочетание двух подходов: применение одной схемы не исключает использования другой.   
  
В состав платформы MVC входят следующие компоненты.

[![Ссылаясь на действие контроллера, которое ожидает значение параметра](asp-net-mvc-overview/_static/image1.jpg)](asp-net-mvc-overview/_static/image1.png)

**Рисунок 01**: Ссылка на действие контроллера, которое ожидает значение параметра[(Нажмите, чтобы просмотреть полноразмерное изображение)](asp-net-mvc-overview/_static/image2.png)

- **Модели**. Объекты модели являются частями приложения, которые реализуют логику для домена данных приложения. Объекты моделей часто получают и сохраняют состояние модели в базе данных. Например, объект продукта может получить информацию из базы данных, работать на ней, а затем написать обновленную информацию обратно в таблицу Продуктов в сервере S'L.

В небольших приложениях эта модель подразумевает концептуальное, а не физическое разделение. Например, если приложение читает только набор данных и отправляет его в представление, приложение не имеет физического слоя модели и связанных классов. В этом случае набор данных берет на себя роль объекта модели.

- **Просмотры**. Представления — это компоненты, отображающие пользовательский интерфейс приложения (UI). Пользовательский интерфейс обычно создается на основе данных модели. Примером может быть редактирование представления таблицы Продуктов, отображающая текстовые ящики, списки выпадающих и чековых коробок в зависимости от текущего состояния объекта продуктов.

- **Контроллеры**. Контроллеры осуществляют взаимодействие с пользователем, работу с моделью, а также выбор представления, отображающего пользовательский интерфейс. В приложении MVC представление служит только для отображения информации. Обработку введенных данных, формирование ответа и взаимодействие с пользователем обеспечивает контроллер. Например, контроллер обрабатывает значения строки запроса и передает эти значения модели, что, в свою очередь, запрашивает базу данных с помощью значений.

Шаблон MVC позволяет создавать приложения, различные аспекты которых (логика ввода, бизнес-логика и логика интерфейса) разделены, но достаточно тесно взаимодействуют друг с другом. Эта схема указывает расположение каждого вида логики в приложении. Логика пользовательского интерфейса относится к представлению. Логика ввода относится к контроллеру. Бизнес-логика размещается в модели. Это разделение позволяет работать со сложными структурами при создании приложения, так как обеспечивает одновременную реализацию только одного аспекта. Например, разработчик может сконцентрироваться на создании представления отдельно от бизнес-логики.   
  
В дополнение к упрощению сложных структур схема MVC также облегчает тестирование приложений по сравнению с веб-приложениями ASP.NET на основе веб-форм. Например, в веб-приложении ASP.NET на основе веб-форм один класс используется для отображения вывода и для ответа на ввод пользователя. Создание автоматических тестов для приложений ASP.NET на основе веб-форм может представлять сложности, так как для тестирования отдельной страницы следует создать экземпляр класса страницы, всех дочерних элементов управления и других зависимых классов приложения. Большое число экземпляров классов, необходимое для запуска страницы, усложняет создание тестов для отдельных частей приложения. Из-за этого тестирование приложений ASP.NET на основе веб-форм может быть сложнее тестирования приложения MVC. Более того, для тестирования приложения ASP.NET необходим веб-сервер. Платформа MVC разделяет компоненты и активно использует интерфейсы, что позволяет тестировать отдельные элементы вне остальной структуры.   
  
Связь между основными компонентами приложения MVC также облегчает параллельную разработку. Например, один разработчик может работать над представлением, второй разработчик может работать над логикой контроллера, а третий — на бизнес-логике в модели.

## <a name="deciding-when-to-create-an-mvc-application"></a>Решение о создании приложения MVC

Следует внимательно продумать вопрос о создании веб-приложения на основе платформы ASP.NET MVC или на основе модели веб-форм ASP.NET. Платформа MVC не заменяет собой модель веб-форм. Обе модели можно использовать для веб-приложений. (при наличии существующих приложений на основе веб-форм они будут продолжать работу в нормальном режиме).   
  
Перед использованием платформы MVC или модели веб-форм для определенного веб-сайта следует взвесить все преимущества каждого из подходов.

### <a name="advantages-of-an-mvc-based-web-application"></a>Преимущества веб-приложения на основе MVC

Платформа ASP.NET MVC имеет следующие преимущества.

- Она облегчает управление сложными структурами путем разделения приложения на модель, представление и контроллер.
- Она не использует состояние просмотра и серверные формы. Это делает платформу MVC идеальной для разработчиков, которым необходим полный контроль над поведением приложения.
- Она использует схему основного контроллера, при которой запросы веб-приложения обрабатываются через один контроллер. Это позволяет создавать приложения, поддерживающие расширенную инфраструктуру маршрутизации. Для получения дополнительной информации [см.](https://go.microsoft.com/fwlink/?LinkId=106357 "Передний контроллер")
- Она обеспечивает расширенную поддержку разработки на основе тестирования.
- Он хорошо работает для веб-приложений, которые поддерживаются большими командами разработчиков и веб-дизайнеров, которым требуется высокая степень контроля над поведением приложений.

### <a name="advantages-of-a-web-forms-based-web-application"></a>Преимущества веб-приложения на основе веб-форм

Платформа на основе веб-форм имеет следующие преимущества.

- Она поддерживает модель событий, которая сохраняет состояние при передаче через HTTP, что облегчает разработку бизнес веб-приложений. Приложение на основе веб-форм предоставляет множество событий, поддерживаемых различными серверными элементами управления.
- Она использует шаблон контроллера страницы, добавляющий функции к отдельным страницам. Для получения дополнительной информации смотрите [Контроллер Страницы](https://go.microsoft.com/fwlink/?LinkId=106359 "Контроллер страниц") на веб-сайте MSDN.
- Он использует формы состояния представления или сервера, которые могут упростить управление информацией о состоянии.
- Она подходит для небольших коллективов веб-разработчиков, которым необходимо использовать большое количество компонентов для быстрого развертывания приложений.
- Как правило, он менее сложен для разработки приложений, поскольку компоненты (класс **Страницы,** элементы управления и т.д.) плотно интегрированы и обычно требуют меньше кода, чем модель MVC.

## <a name="features-of-the-aspnet-mvc-framework"></a>Возможности платформы ASP.NET MVC

Платформа ASP.NET MVC предоставляет следующие возможности.

- Разделение задач приложений (логика ввода, бизнес-логика и логика uI), тестируемость и разработка на основе тестов (TDD) по умолчанию. Все основные контракты платформы MVC основаны на интерфейсе и подлежат тестированию с помощью макетов объекта, которые имитируют поведение реальных объектов приложения. Приложение можно подвергать модульному тестированию без запуска контроллеров в процессе ASP.NET, что ускоряет тестирование и делает его более гибким. Для тестирования возможно использование любой платформы модульного тестирования, совместимой с .NET Framework.
- Расширяемая и дополняемая платформа. Компоненты платформы ASP.NET MVC можно легко заменить или настроить. Разработчик может подключать собственный механизм представлений, политику маршрутизации URL-адресов, сериализацию параметров методов действий и другие компоненты. Платформа ASP.NET MVC также поддерживает использование моделей контейнера внедрения зависимости (DI) и инверсии элемента управления (IOC). DI позволяет вводить объекты в класс, вместо того, чтобы полагаться на класс для создания самого объекта. Модель инверсии элемента управления указывает на то, что если один объект требует другой объект, то первые объекты должны получить второй объект из внешнего источника (например, из файла конфигурации). Это облегчает тестирование.
- Мощный компонент отображения URL, который позволяет создавать приложения с понятными и поисковыми URL-адресами. URL-адреса не должны содержать расширения имен файлов и предназначены для поддержки шаблонов именования URL-адресов, обеспечивающих адресацию, оптимизированную для поисковых систем (SEO) и для передачи репрезентативного состояния (REST).
- Поддержка использования разметки в существующих файлах страниц ASP.NET (ASPX), элементов управления (ASCX) и главных страниц (MASTER) как шаблонов представлений. Существующие ASP.NET функции с ASP.NET mVC, такие как вложенные мастер-страницы, линейные выражения (% -&lt;%&gt;), декларативные элементы управления сервером, шаблоны, связывание данных, локализация и так далее.
- Поддержка существующих функций ASP.NET. ASP.NET MVC позволяет использовать такие функции, как проверка подлинности с помощью форм и Windows, проверка подлинности по URL-адресу, членство и роли, кэширование вывода и данных, управление состоянием сеанса и профиля, наблюдение за работоспособностью, система конфигурации и архитектура поставщика.
