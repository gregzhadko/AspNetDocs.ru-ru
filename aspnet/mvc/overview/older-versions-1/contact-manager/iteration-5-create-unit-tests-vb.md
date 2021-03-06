---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
title: 'Итерация #5 - Создание модульных тестов (VB) Документы Майкрософт'
author: rick-anderson
description: В пятой итерации мы упрощаем обслуживание и модификацию нашего приложения путем добавления модульных тестов. Мы издеваемся над нашими классами моделей данных и строим модульные тесты для o. .
ms.author: riande
ms.date: 02/20/2009
ms.assetid: c6e5c036-2265-4fa7-a9eb-47f197bdc262
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
msc.type: authoredcontent
ms.openlocfilehash: cc5425de86e7481894fbea242fa555b5598167f6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542343"
---
# <a name="iteration-5--create-unit-tests-vb"></a>Итерация 5. Создание модульных тестов (VB)

[корпорацией Майкрософт](https://github.com/microsoft)

[Скачать код](iteration-5-create-unit-tests-vb/_static/contactmanager_5_vb1.zip)

> В пятой итерации мы упрощаем обслуживание и модификацию нашего приложения путем добавления модульных тестов. Мы издеваемся над нашими классами моделей данных и строим модульные тесты для наших контроллеров и логики проверки.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Создание приложения управления контактами ASP.NET MVC (VB)

В этой серии учебников мы создаем все приложение Управления Контактами от начала до конца. Приложение Contact Manager позволяет хранить контактную информацию - имена, номера телефонов и адреса электронной почты - для списка людей.

Мы строим приложение по нескольким итерациям. С каждой итерацией мы постепенно совершенствуем приложение. Цель этого подхода с множественной итерацией состоит в том, чтобы вы могли понять причину каждого изменения.

- Итерация #1 - Создайте приложение. В первой итерации мы создаем Контакт-менеджер самым простым способом. Мы добавляем поддержку для основных операций базы данных: Создание, чтение, обновление и удаление (CRUD).

- Итерация #2 - Сделать приложение хорошо выглядеть. В этой итерации мы улучшаем внешний вид приложения, изменяя страницу по умолчанию ASP.NET MVC просмотра и каскадный стиль листа.

- Итерация #3 - Добавить проверку формы. В третьей итерации мы добавляем базовую проверку формы. Мы не позволяем людям подавать форму без заполнения требуемых полей формы. Мы также проверяем адреса электронной почты и номера телефонов.

- Итерация #4 - Сделать приложение слабо связаны. В этой четвертой итерации мы воспользуемся несколькими шаблонами проектирования программного обеспечения, чтобы упростить обслуживание и изменение приложения Contact Manager. Например, мы рефакторизуем наше приложение, чтобы использовать шаблон репозитория и шаблон инъекций зависимостей.

- Итерация #5 - Создание модульных тестов. В пятой итерации мы упрощаем обслуживание и модификацию нашего приложения путем добавления модульных тестов. Мы издеваемся над нашими классами моделей данных и строим модульные тесты для наших контроллеров и логики проверки.

- Итерация #6 - Использование тест-ориентированной разработки. В этой шестой итерации мы добавляем новую функциональность в наше приложение, написав модульные тесты сначала и написав код против модульных тестов. В этой итерации мы добавляем контактные группы.

- Итерация #7 - Добавить функциональность Ajax. В седьмой итерации мы улучшаем отзывчивость и производительность нашего приложения, добавляя поддержку Ajax.

## <a name="this-iteration"></a>Эта итерация

В предыдущей итерации приложения Contact Manager мы рефакторинг приложения, чтобы быть более свободно связаны. Мы разделили приложение на отдельные слои контроллера, обслуживания и репозитория. Каждый слой взаимодействует с слоем под ним через интерфейсы.

Мы рефакторинг приложения, чтобы сделать приложение проще в обслуживании и изменении. Например, если нам необходимо использовать новую технологию доступа к данным, мы можем просто изменить слой репозитория, не касаясь контроллера или такого слоя. Делая Контакт-менеджер слабо связаны, мы сделали приложение более устойчивым к изменениям.

Но что происходит, когда нам нужно добавить новую функцию в приложение Contact Manager? Или, что происходит, когда мы исправляем ошибку? Грустная, но хорошо доказанная истина написания кода заключается в том, что всякий раз, когда вы касаетесь кода, вы создаете риск введения новых ошибок.

Например, в один прекрасный день менеджер может попросить вас добавить новую функцию в Контакт-менеджер. Она хочет, чтобы вы добавили поддержку Контактным группам. Она хочет, чтобы вы могли позволить пользователям организовывать свои контакты в такие группы, как Друзья, Бизнес и так далее.

Для реализации этой новой функции необходимо изменить все три слоя приложения Contact Manager. Необходимо добавить новую функциональность в контроллеры, уровень обслуживания и репозиторий. Как только вы начнете изменять код, вы рискуете взломать функциональность, которая работала раньше.

Рефакторинг нашего приложения в отдельные слои, как мы это делали в предыдущей итерации, было хорошо. Это было хорошо, потому что это позволяет нам вносить изменения в целые слои, не касаясь остальной части приложения. Однако, если вы хотите упростить обслуживание и изменение кода в слое слоя, необходимо создать модульные тесты для кода.

Для тестирования отдельной единицы кода используется модульный тест. Эти единицы кода меньше, чем целые слои приложений. Как правило, используется модульный тест для проверки того, ведет ли тот или иной метод в коде то, что вы ожидаете. Например, можно создать модульный тест для метода CreateContact(), выставленный классом ContactManagerService.

Модульные тесты для приложения работают так же, как защитная сетка. Всякий раз, когда вы изменяете код в приложении, вы можете запустить набор модульных тестов, чтобы проверить, нарушает ли изменение существующую функциональность. Единие тесты делают ваш код безопасным для изменения. Единие тесты делают весь код в приложении более устойчивым к изменениям.

В этой итерации мы добавляем модульные тесты в наше приложение Contact Manager. Таким образом, в следующей итерации мы можем добавить Контактные группы в наше приложение, не беспокоясь о нарушении существующей функциональности.

> [!NOTE] 
> 
> Существует множество инфраструктур модульного тестирования, включая NUnit, xUnit.net и MbUnit. В этом учебнике мы используем платформу модульного тестирования, включенную в Visual Studio. Тем не менее, вы можете так же легко использовать одну из этих альтернативных инфраструктур.

## <a name="what-gets-tested"></a>Что проходит тестирование

В идеальном мире весь ваш код будет покрыт модульными тестами. В идеальном мире, вы бы идеальный сетки безопасности. Вы сможете изменить любую строку кода в приложении и мгновенно узнать, вырабатывая модульные тесты, нарушило ли изменение существующую функциональность.

Тем не менее, мы не живем в идеальном мире. На практике при написании модульных тестов вы концентрируетесь на написании тестов для бизнес-логики (например, логики проверки). В частности, вы *не* пишете модульные тесты для логики доступа к данным или логики представления.

Чтобы быть полезным, модульные тесты должны выполняться очень быстро. Вы легко можете накопить сотни (или даже тысячи) модульных тестов для приложения. Если модульные тесты займут много времени, то вы избежите их выполнения. Другими словами, длительные модульные тесты бесполезны для повседневных целей кодирования.

По этой причине обычно вы не пишете модульные тесты для кода, который взаимодействует с базой данных. Запуск сотен модульных тестов против живой базы данных будет слишком медленным. Вместо этого вы издеваетесь над базой данных и пишете код, который взаимодействует с базой данных макетов (мы обсуждаем насмешки над базой данных ниже).

По аналогичной причине обычно не записывается модульные тесты для представлений. Для проверки представления необходимо раскрутить веб-сервер. Поскольку закрутка веб-сервера является относительно медленным процессом, создание модульных тестов для ваших представлений не рекомендуется.

Если представление содержит сложную логику, то следует рассмотреть вопрос о перемещении логики в методы Helper. Вы можете написать модульные тесты для методов Helper, которые выполняются без вращения веб-сервера.

> [!NOTE] 
> 
> При написании тестов для логики доступа к данным или логики представления не очень хорошая идея при написании модульных тестов, эти тесты могут быть очень ценными при построении функциональных или интеграционных тестов.

> [!NOTE] 
> 
> ASP.NET MVC — это движок представления веб-форм. В то время как Web Forms View Engine зависит от веб-сервера, другие двигатели представления могут и не быть.

## <a name="using-a-mock-object-framework"></a>Использование рамочной программы мок-объектов

При создании модульных тестов почти всегда необходимо использовать фреймворк Mock Object. Платформа Mock Object позволяет создавать макеты и заглушки для классов в приложении.

Например, можно использовать платформу Mock Object для создания макетной версии класса репозитория. Таким образом, вы можете использовать класс макетов репозитория вместо реального класса репозитория в модульных тестах. Использование макетного репозитория позволяет избежать выполнения кода базы данных при выполнения модульного теста.

Visual Studio не включает в себя платформу Mock Object. Однако для платформы .NET доступно несколько коммерческих и открытых исходных кодов, доступных для платформы .NET:

1. Moq - Эта платформа доступна под лицензией BSD с открытым исходным кодом. Вы можете скачать [https://code.google.com/p/moq/](https://code.google.com/p/moq/)Moq от .
2. Rhino Mocks - Эта платформа доступна под лицензией BSD с открытым исходным кодом. Вы можете скачать [http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx)Rhino Mocks из .
3. Typemock Isolator - Это коммерческая структура. Вы можете скачать [http://www.typemock.com/](http://www.typemock.com/)пробную версию из .

В этом учебнике, я решил использовать Moq. Тем не менее, вы можете так же легко использовать Rhino Mocks или Typemock Isolator для создания объектов Mock для приложения Contact Manager.

Прежде чем использовать Moq, необходимо выполнить следующие шаги:

1. .
2. Перед тем, как распаковать загрузку, убедитесь, что вы правой кнопкой мыши файла и нажмите кнопку помечены **Разблокировать** (см. Рисунок 1).
3. Unzip загрузки.
4. Добавьте ссылку на сборку Moq в свой тестовый проект, выбрав вариант меню **Project, добавьте ссылку,** чтобы открыть диалог **Add Reference.** Под вкладкой «Обзор» просмотрите папку, где расстегнули Moq, и выберите сборку Moq.dll. Нажмите кнопку **ОК** (см. рисунок 2).

[![Разблокирование Moq](iteration-5-create-unit-tests-vb/_static/image1.jpg)](iteration-5-create-unit-tests-vb/_static/image1.png)

**Рисунок 01**: Разблокировка Moq[(Нажмите, чтобы посмотреть полноразмерное изображение](iteration-5-create-unit-tests-vb/_static/image2.png))

[![Ссылки после добавления Moq](iteration-5-create-unit-tests-vb/_static/image2.jpg)](iteration-5-create-unit-tests-vb/_static/image3.png)

**Рисунок 02**: Ссылки после добавления Moq[(Нажмите, чтобы просмотреть полноразмерное изображение](iteration-5-create-unit-tests-vb/_static/image4.png))

## <a name="creating-unit-tests-for-the-service-layer"></a>Создание модульных тестов для уровня обслуживания

Начнем с создания набора модульных тестов для нашего сервисного слоя приложения Contact Manager. Мы будем использовать эти тесты для проверки нашей логики проверки.

Создайте новую папку под названием Модели в проекте ContactManager.Tests. Далее, правой кнопкой кнопку Модели папку и выберите **Добавить, Новый тест**. Отображается диалог **Добавить новый тест,** показанный на рисунке 3. Выберите шаблон **Unit Test** и назовите новый тест ContactManagerServiceTest.vb. Нажмите кнопку **OK,** чтобы добавить новый тест в тестовый проект.

> [!NOTE] 
> 
> Как правило, требуется, чтобы структура папок вашего тестового проекта соответствовала структуре папок вашего проекта ASP.NET MVC. Например, вы размещаете тесты контроллеров в папке контроллеров, тесты моделей в папке Модели и так далее.

[![Модели-КонтактМенеджерСервисТест.cs](iteration-5-create-unit-tests-vb/_static/image3.jpg)](iteration-5-create-unit-tests-vb/_static/image5.png)

**Рисунок 03**: Модели»ContactManagerServiceTest.cs[(Нажмите, чтобы просмотреть полноразмерное изображение](iteration-5-create-unit-tests-vb/_static/image6.png))

Первоначально мы хотим протестировать метод CreateContact(), выставленный классом ContactManagerService. Мы создадим следующие пять тестов:

- CreateContact() - Тесты, которые CreateContact() возвращает значение истинное, когда действительный контакт передается методу.
- CreateContactRequiredFirstName() - Тесты добавления сообщения об ошибке в состояние модели при перекаче контакта с отсутствующим именем методу CreateContact().
- CreateContactRequiredLastName() - Тесты добавления сообщения об ошибке в состояние модели при перекаче контакта с отсутствующим и фамилией в метод CreateContact().
- CreateContactInvalidPhone() - Тесты, что сообщение об ошибке добавляется в состояние модели, когда контакт с недействительным номером телефона передается методу CreateContact().
- CreateContactInvalidEmail() - Тесты, что сообщение об ошибке добавляется в состояние модели, когда контакт с недействительным адресом электронной почты передается методу CreateContact() .

Первый тест проверяет, что допустимый Контакт не генерирует ошибку проверки. Остальные тесты проверяют каждое из правил проверки.

Код для этих тестов содержится в листинге 1.

**Список 1 - Модели/ContactManagerServiceTest.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample1.vb)]

Поскольку мы используем класс Контактов в листинге 1, нам необходимо добавить ссылку на рамку сущности Майкрософт к нашему тестовому проекту. Добавьте ссылку на сборку System.Data.Entity.

Список 1 содержит метод под названием Initialize(), который украшен атрибутом «Test Initialize». Этот метод вызывается автоматически перед запуском каждого из модульных тестов (он называется 5 раз прямо перед каждым из модульных тестов). Метод Инициализации () создает макет репозитория со следующей строкой кода:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample2.vb)]

Эта строка кода использует платформу Moq для создания макетного репозитория из интерфейса IContactManagerRepository. Макет репозитория используется вместо фактического EntityContactManagerRepository, чтобы избежать доступа к базе данных, когда каждый модульный тест запущен. Макет репозитория реализует методы интерфейса IContactManagerRepository, но методы на самом деле не делают ничего.

> [!NOTE] 
> 
> При использовании фрекинга Moq \_существует различие между \_mockRepository и mockRepository.Object. Первый относится к классу Mock (Of IContactManagerRepository), который содержит методы определения того, как будет вести себя макет репозиторий. Последний относится к фактическому репозиторию макетов, который реализует интерфейс IContactManagerRepository.

Макет репозитория используется в методе Инициализации () при создании экземпляра класса ContactManagerService. Все отдельные модульные тесты используют этот экземпляр класса ContactManagerService.

Список 1 содержит пять методов, которые соответствуют каждому из модульных тестов. Каждый из этих методов украшен атрибутом «TestMethod». При запуске модульных тестов вызывается любой метод, который имеет этот атрибут. Другими словами, любой метод, украшенный атрибутом «TestMethod», является модульным тестом.

Первый модульный тест, названный CreateContact(, проверяет, что вызов CreateContact() возвращает истинное значение при передаваемых методу допустимого экземпляра класса Контакт. Тест создает экземпляр класса Контакт, вызывает метод CreateContact() и проверяет, что CreateContact() возвращает значение истинное.

Остальные тесты проверяют, что при вызове метода CreateContact() с недействительным контактом, затем метод возвращается ложным, и ожидаемое сообщение об ошибке проверки добавляется в состояние модели. Например, тест CreateContactRequiredFirstName() создает экземпляр класса Контакт с пустой строкой для свойства FirstName. Далее метод CreateContact() вызывается с недействительным контактом. Наконец, тест проверяет, что CreateContact() возвращает ложно, и что состояние модели содержит ожидаемое сообщение об ошибке проверки "Требуется первое имя".

Вы можете запустить модульные тесты в листинге 1, выбрав вариант меню **Тест, Выполнить, Все тесты в решении (CTRL-R, A)**. Результаты тестов отображаются в окне результатов тестирования (см. рисунок 4).

[![Результаты тестирования](iteration-5-create-unit-tests-vb/_static/image4.jpg)](iteration-5-create-unit-tests-vb/_static/image7.png)

**Рисунок 04**: Результаты испытаний[(Нажмите, чтобы просмотреть полноразмерное изображение)](iteration-5-create-unit-tests-vb/_static/image8.png)

## <a name="creating-unit-tests-for-controllers"></a>Создание модульных тестов для контроллеров

ASP.NET приложение MVC контролирует поток взаимодействия с пользователем. При тестировании контроллера необходимо проверить, возвращает ли контроллер нужный результат действия и просматривать данные. Также можно проверить, взаимодействует ли контроллер с классами моделей в ожидаемом порядке.

Например, листинг 2 содержит два модульных теста для метода создания контроллера контакта() . Первый модульный тест проверяет, что при перекачном контакте в метод «Создание() — метод Create() перенаправляет сявок в действие Индекса. Другими словами, при пройдении действительного контакта метод Create() должен вернуть RedirectToRouteResult, представляющий действие Индекса.

Мы не хотим тестировать уровень обслуживания ContactManager при тестировании слоя контроллера. Поэтому мы издеваемся над уровнем обслуживания со следующим кодом в методе Инициализации:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample3.vb)]

В модульном тесте CreateValidContact() мы издеваемся над поведением вызова метода CreateContact() со следующей строкой кода:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample4.vb)]

Эта строка кода заставляет макет службы ContactManager вернуть значение истинное, когда называется его метод CreateContact.) Высмеивая уровень обслуживания, мы можем проверить поведение нашего контроллера без необходимости выполнения какого-либо кода в уровне обслуживания.

Второй модульный тест проверяет, что действие Create() возвращает представление Create при перекачном контакте с недействительным контактом с методом. Мы заставляют метод CreateContact() создать() метод возврата значения ложным со следующей строкой кода:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample5.vb)]

Если метод Create() ведет себя так, как мы ожидаем, он должен вернуть представление Create, когда слой службы возвращает ложное значение. Таким образом, контроллер может отображать сообщения об ошибке проверки в представлении Create, и у пользователя есть шанс исправить эти недействительные свойства контакта.

Если вы планируете создавать модульные тесты для контроллеров, то вам нужно вернуть явные имена представлений из действий контроллера. Например, не возвращайте представление следующим образом:

Обратный вид()

Вместо этого верните представление следующим образом:

Просмотр возврата ("Создание")

Если вы не явны при возврате представления, то свойство ViewResult.ViewName возвращает пустую строку.

**Список 2 - Контроллеры/ContactControllerTest.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample6.vb)]

## <a name="summary"></a>Сводка

В этой итерации мы создали модульные тесты для нашего приложения Contact Manager. Мы можем запустить эти модульные тесты в любое время, чтобы убедиться, что наше приложение по-прежнему ведет себя так, как мы ожидаем. Модульные тесты служат защитной сеткой для нашего приложения, что позволяет нам безопасно изменять наше приложение в будущем.

Мы создали два набора модульных тестов. Во-первых, мы проверили нашу логику проверки, создав модульные тесты для нашего сервисного слоя. Затем мы протестировали логику управления потоком, создав модульные тесты для нашего слоя контроллера. При тестировании нашего уровня обслуживания мы изолировали наши тесты для нашего слоя службы от нашего слоя репозитория, насмехаясь над нашим слоем репозитория. При тестировании слоя контроллера мы изолировали наши тесты для нашего слоя контроллера, высмеивая уровень обслуживания.

В следующей итерации мы модифицировали приложение Contact Manager таким образом, чтобы оно поддерживало Контактные группы. Мы добавим эту новую функциональность в наше приложение, используя процесс разработки программного обеспечения, называемый разработкой, управляемой тестами.

> [!div class="step-by-step"]
> [Назад](iteration-4-make-the-application-loosely-coupled-vb.md)
> [Вперед](iteration-6-use-test-driven-development-vb.md)
