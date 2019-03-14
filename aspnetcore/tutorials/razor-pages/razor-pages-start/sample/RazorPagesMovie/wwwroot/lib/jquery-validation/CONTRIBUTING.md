---
ms.openlocfilehash: 3b33bb9bcab1aa7e5438c6fe3f2d7ba0833e7756
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57060821"
---
--

## <a name="reporting-an-issue"></a>Сообщение о проблеме

1. Убедитесь, что ваша проблема воспроизводима.
2. Используйте http://jsbin.com или http://jsfiddle.net для предоставления тестовой страницы.
3. Укажите браузеры, в которых можно воспроизвести эту проблему. **Примечание. Неполадки в режиме совместимости с IE не будут устранены. Убедитесь в том, что выполняете тестирование в реальном браузере!**
4. В какой версии подключаемого модуля можно воспроизвести проблему? Можно ли ее воспроизвести после обновления до последней версии?

Вопросы, касающиеся документации, также отслеживаются с помощью средства отслеживания проблем [проверки jQuery](https://github.com/jzaefferer/jquery-validation/issues).
Тем не менее вы можете отправлять запросы на вытягивание для улучшения документов в репозитории с [документацией по проверке jQuery](https://github.com/jzaefferer/validation-content).

**ВАЖНОЕ ПРИМЕЧАНИЕ О ПРОВЕРКЕ ЭЛЕКТРОННОЙ ПОЧТЫ**. Начиная с версии 1.12.0, этот подключаемый модуль использует то же регулярное выражение, которое [предлагает использовать спецификация HTML5 для браузеров](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address). Мы будем следовать этому примеру и используем ту же проверку. Если вы считаете, что спецификация неправильная, обратитесь к специалистам и сообщите о проблеме. Если у вас есть различные требования, рассмотрите [использование настраиваемого метода](http://jqueryvalidation.org/jQuery.validator.addMethod/).

## <a name="contributing-code"></a>Код дополнения

Благодарим за дополнение! Вот несколько рекомендаций, которые помогут вам разместить дополнение.

1. Убедитесь, что ваша проблема воспроизводима. Используйте jsbin.com или jsfiddle.net, чтобы указать тестовую страницу.
2. Следуйте указаниям в [руководстве по стилю jQuery](http://contribute.jquery.com/style-guides/js)
3. Добавьте или обновите модульные тесты вместе с вашим исправлением. Выполните модульные тесты как минимум в одном браузере (см. ниже).
4. Запустите `grunt` (см. ниже), чтобы проверить наличие выделения и некоторых других проблем.
5. Опишите изменения в своем сообщении фиксации и ссылайтесь на запрос следующим образом: «Демонстрации: Исправлена ошибка делегирования для демонстрации динамических итогов. Исправления №51". Если вы добавляете новый файл локализации, используйте примерно следующее: «Локализации: Добавлена Хорватский (HR) локализация»

## <a name="build-setup"></a>Установка сборки

1. Установите [NodeJS](http://nodejs.org).
2. Установите интерфейс командной строки Grunt, выполнив `npm install -g grunt-cli`. Дополнительные сведения доступны на веб-сайте http://gruntjs.com/getting-started.
3. Установите зависимости NPM, запустив `npm install`.
4. Сейчас сборку можно вызвать, запустив `grunt`.

## <a name="creating-a-new-additional-method"></a>Создание дополнительного метода

Если вам нужно добавить пользовательские методы к additional-methods.js, сделайте следующее:

1. Создание ветви
2. Добавьте метод в качестве нового файла в `src/additional`.
3. Добавьте переводы в `src/localization` (необязательно).
4. Отправьте запрос на вытягивание в главную ветвь.

## <a name="unit-tests"></a>Модульные тесты

Для выполнения модульных тестов просто откройте `test/index.html` в браузере. Запустите `npm install`, чтобы все необходимые зависимости были доступны.
Начните с одного браузера при разработке исправления, а затем запустите его в других перед отправкой. Как правило, это последние версии Chrome, Firefox, Safari, Opera и несколько IE.

## <a name="documentation"></a>Документация

Задавайте вопросы, касающиеся документации, в средстве отслеживания проблем [проверки jQuery](https://github.com/jzaefferer/jquery-validation/issues).
Если ваш запрос на вытягивание реализует или изменяет открытый API, было бы неплохо отправить его в репозиторий с [документацией по проверке jQuery](https://github.com/jzaefferer/validation-content).

## <a name="linting"></a>Выделение

Чтобы запустить JSHint и другие средства, используйте `grunt`.