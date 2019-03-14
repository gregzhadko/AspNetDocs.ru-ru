---
title: ASP.NET Core нагрузки/нагрузочное тестирование
author: Jeremy-Meng
description: Описывает несколько важные средства и способы нагрузочное тестирование и нагрузочное тестирование приложений ASP.NET Core.
ms.author: riande
ms.custom: mvc
ms.date: 01/04/2019
uid: test/loadtests
ms.openlocfilehash: d989bc841a372bed7ebf2c84c6abe1a57762ad04
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061411"
---
# <a name="load-and-stress-testing-aspnet-core"></a>Нагрузочное тестирование ASP.NET Core

Нагрузочное тестирование и нагрузочное тестирование, важно убедиться, что веб-приложения обеспечивает высокую производительность и масштабируемость. Поставленных целей отличаются даже часто имеют похожих тестов.

**Нагрузочные тесты**: Проверяет, является ли приложение могло обработать указанный нагрузки пользователей для определенного сценария, поддерживая их ответа. Приложение выполняется в обычных условиях.

**Нагрузочные тесты**: Тесты стабильности приложения, при выполнении в экстремальных условиях и часто длительного периода времени:

* Высокая нагрузка — пики или постепенно увеличивается.
* Ограниченные вычислительные ресурсы.  

Под нагрузкой можно его восстановление после сбоя и корректно вернуться к ожидаемое поведение? Под нагрузкой, приложение будет *не* выполнения в нормальных условиях.

## <a name="visual-studio-tools"></a>Инструменты Visual Studio

Visual Studio позволяет пользователям создавать, разрабатывать и отлаживать веб-производительности и нагрузочных тестов. Доступно для создания тестов путем записи действий в веб-браузере.

[Краткое руководство. Создание проекта нагрузочного тестирования](/visualstudio/test/quickstart-create-a-load-test-project?view=vs-2017) показано, как создание, Настройка и Запуск нагрузочного теста с помощью Visual Studio 2017 проектов.

См. [Дополнительные ресурсы](#add).

Нагрузочные тесты можно настроить для запуска в локальном или запуска в облаке, с помощью DevOps в Azure.

## <a name="azure-devops"></a>Azure DevOps

Нагрузочных тестов можно запустить с помощью [Azure DevOps планов тестирования](/azure/devops/test/load-test/index?view=vsts) службы.

![](./load-tests/_static/azure-devops-load-test.png)

Служба поддерживает следующие типы формата теста:

- Тест Visual Studio — веб-теста, созданных в Visual Studio.
- Тестов на основе архива HTTP — записанный HTTP-трафик в архив воспроизводится во время тестирования.
- [Тестов на основе URL-адрес](/azure/devops/test/load-test/get-started-simple-cloud-load-test?view=vsts) — позволяет указать URL-адреса, чтобы загрузить тест, типы запросов, заголовки и строки запросов. Запустить задание параметров, таких как длительность, шаблон нагрузки, пользователей и т. д., можно настроить.
- [Apache JMeter](https://jmeter.apache.org/) тестирования.

## <a name="azure-portal"></a>порталу Azure

[Портал Azure предоставляет настройки и выполнения нагрузочного тестирования веб-приложений,](/azure/devops/test/load-test/app-service-web-app-performance-test?view=vsts) напрямую из вкладки производительности службы приложений на портале Azure.

![](./load-tests/_static/azure-appservice-perf-test.png)

Тест может быть ручного теста с указанным URL-адрес или файл веб-тест Visual Studio, который можно проверить несколько URL-адресов.

![](./load-tests/_static/azure-appservice-perf-test-config.png)

В конце теста отчеты создаются для отображения характеристик производительности приложения. Пример Статистика включает в себя:

- Среднее время отклика
- Макс. пропускная способность: запросов в секунду
- Процент неудачных

## <a name="third-party-tools"></a>Сторонние средства

Следующий список содержит средства обеспечения производительности сторонних разработчиков с различных наборов функций:

- [Apache JMeter](https://jmeter.apache.org/) : Полный набор избранные средства тестирования нагрузки. Привязана к потоку: требуется один поток для каждого пользователя.
- [AB - сервер Apache HTTP, средство тестирования](https://httpd.apache.org/docs/2.4/programs/ab.html)
- [Gatling](https://gatling.io/) : Программы рабочего стола с помощью средства графического пользовательского интерфейса и тестирования для записи. Более высокую производительность, чем JMeter.
- [Locust.IO](https://locust.io/) : Не ограничено потоков.

<a name="add"></a>
## <a name="additional-resources"></a>Дополнительные ресурсы

[Серия записей блога теста нагрузки](https://blogs.msdn.microsoft.com/charles_sterling/2015/06/01/load-test-series-part-i-creating-web-performance-tests-for-a-load-test/) по (Charles Sterling). Выпущенное, но большинство из разделов по-прежнему актуальны.