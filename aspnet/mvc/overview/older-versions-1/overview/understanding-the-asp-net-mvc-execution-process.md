---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: Понимание процесса ASP.NET выполнения MVC (ru) Документы Майкрософт
author: rick-anderson
description: Узнайте, как ASP.NET mVC-платформа обрабатывает запрос браузера шаг за шагом.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541030"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a>Общие сведения о процессе выполнения ASP.NET MVC

[корпорацией Майкрософт](https://github.com/microsoft)

> Узнайте, как ASP.NET mVC-платформа обрабатывает запрос браузера шаг за шагом.

Запросы на ASP.NET веб-приложении на основе MVC сначала проходят через объект **UrlRoutingModule,** который является модулем HTTP. Этот модуль анализирует запрос и выбирает маршрут. Объект **UrlRoutingModule** выбирает первый объект маршрута, который соответствует текущему запросу. (Объект маршрута — это класс, реализуемый **routeBase**и обычно который является экземпляром класса **Route.)** Если маршруты не совпадают, объект **UrlRoutingModule** ничего не делает и позволяет запросу вернуться к обычной обработке запроса ASP.NET или IIS.

Из выбранного объекта **Маршрута** объект **UrlRoutingModule** получает объект **IRouteHandler,** связанный с объектом **Маршрута.** Как правило, в приложении MVC это будет экземпляр **MvcRouteHandler.** Экземпляр **IRouteHandler** создает объект **IHttpHandler** и передает его **объектi IHttpContext.** По умолчанию экземпляр **IHttpHandler** для MVC является объектом **MvcHandler.** Затем объект **MvcHandler** выбирает контроллер, который в конечном итоге будет обрабатывать запрос.

> [!NOTE]
> Если веб-приложение ASP.NET на базе MVC запускается в IIS 7.0, для проектов MVC не требуется расширение имени файла. В IIS 6.0 для обработки необходимо, чтобы расширение имени файла MVC было связано с библиотекой DLL ISAPI ASP.NET.

Модуль и обработчик являются точками входа в ASP.NET mVC. Они отвечают за следующее:

- Выбор нужного контроллера в веб-приложении MVC.
- Получение отдельного экземпляра контроллера.
- Вызов **исчергивайте** метод выполнения контроллера.

Ниже перечислены этапы выполнения для проекта MVC Web:

- Получение первого запроса к приложению. 

    - В файле Global.asax объекты **маршрута** добавляются к объекту **RouteTable.**
- Выполнение маршрутизации 

    - Модуль **UrlRoutingModule** использует первый объект сопоставления **маршрута** в коллекции **RouteTable** для создания объекта **RouteData,** который он затем использует для создания объекта **RequestContext** **(IHttpContext).**
- Создание обработчика запроса MVC 

    - Объект **MvcRouteHandler** создает экземпляр класса **MvcHandler** и передает экземпляр экземпляра **RequestContext.**
- Создание контроллера 

    - Объект **MvcHandler** использует экземпляр **RequestContext** для идентификации объекта **IControllerFactory** (обычно экземпляра класса **DefaultControllerFactory)** для создания экземпляра контроллера.
- Выполняет контроллер - экземпляр **MvcHandler** вызывает метод **выполнения** контроллера. |
- Вызов действия 

    - Большинство контроллеров наследуют из базового класса **контроллера.** Для контроллеров, которые делают это, объект **ControllerActionInvoker,** связанный с контроллером, определяет, какой метод действия класса контроллера вызывает, а затем вызывает этот метод.
- Выполнение результата 

    - Типичный метод действия может получать пользовательский ввод, готовить соответствующие данные ответа, а затем выполнять результат, возвращая тип результата. Встроенные типы результатов, которые могут быть выполнены, включают в себя следующие: **ViewResult** (который отображает представление и является наиболее часто используемым типом результата), **RedirectToRouteResult**, **RedirectResult,** **ContentResult**, **JsonResult**и **EmptyResult.**
