---
ms.openlocfilehash: 4add1c40387073f35711b2c8db27e48657a18192
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061631"
---
# <a name="response-compression-sample-application-aspnet-core-1x"></a>Пример сжатия ответа приложения (ASP.NET Core 1.x)

В этом примере описывается использование ASP.NET Core 1.x по промежуточного слоя для сжатия HTTP-ответы для по сжатия ответов. В примере демонстрируется Gzip и поставщики пользовательских сжатия для ответов, текстом и изображением и показано, как добавить тип MIME для сжатия. Пример ASP.NET Core 2.x, см. в разделе [ответа сжатия пример приложения (ASP.NET Core 2.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples/2.x).

## <a name="examples-in-this-sample"></a>Включенные примеры

* `GzipCompressionProvider`
  * `text/plain`
    * **/** -Lorem Ipsum текстового файла ответа до 2,044 байт, которые будут сжаты до 927 байт
    * **/testfile1kb.txt** -текстового файла ответа до 1,033 байт, которые будут сжаты до 47 байт
    * **/ Тонкая** -ответ, выданный в качестве отдельных символов, с интервалом в 1
  * `image/svg+xml`
    * **/Banner.SVG** — масштабируемый векторный рисунок (SVG) образа реагирование на них 9,707 байтов, которые будут сжаты до 4,459 байт
* `CustomCompressionProvider`<br>Показано, как реализовать поставщик сжатия для использования с по промежуточного слоя

Если запрос содержит `Accept-Encoding` заголовка, в этом примере добавляются `Vary: Accept-Encoding` в ответ заголовок. `Vary` Заголовок указывает кэши, чтобы поддерживать несколько копий ответа на основе альтернативных значений `Accept-Encoding`, поэтому размер несжатой версии и сжатые (gzip) хранятся в кэши для систем, можно либо принять сжатом или несжатый ответ.

## <a name="using-the-sample"></a>Использование образца

1. Запрос с помощью [Fiddler](http://www.telerik.com/fiddler), [Firebug](http://getfirebug.com/), или [Postman](https://www.getpostman.com/) к приложению без `Accept-Encoding` заголовок и Примечание полезные данные ответа, размер ответа, и заголовки ответа.
1. Добавление `Accept-Encoding: gzip` заголовка и обратите внимание на размер сжатого ответа и заголовки ответа. Вы видите drop, размер ответа и `Content-Encoding: gzip` в примере приложения включен заголовок ответа. Если взглянуть на тексте ответа для Lorem Ipsum или **testfile1kb.txt** ответа, вы видите, что текст является сжатые и может быть прочитан.
1. Добавление `Accept-Encoding: mycustomcompression` заголовка и обратите внимание, заголовки ответа. `CustomCompressionProvider` Пустую реализацию, фактически не сжимать ответ, но можно создать оболочку поток сжатия для `CreateStream()` метод.
