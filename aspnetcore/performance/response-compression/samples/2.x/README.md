---
ms.openlocfilehash: 976cc58dfcd9bba0b88ddd5d0d886cbb99b418ae
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026321"
---
# <a name="response-compression-sample-application-aspnet-core-2x"></a>Пример сжатия ответа приложения (ASP.NET Core 2.x)

В этом примере описывается использование ASP.NET Core 2.x по промежуточного слоя сжатия ответов для сжатия HTTP-ответов. В примере демонстрируется Gzip, Brotli и поставщики сжатия для ответов, текстом и изображением и показано, как добавить тип MIME для сжатия. Пример ASP.NET Core 1.x, см. в разделе [ответа сжатия пример приложения (ASP.NET Core 1.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples/1.x).

## <a name="examples-in-this-sample"></a>Включенные примеры

* `BrotliCompressionProvider`
  * `text/plain`
    * **/** -Lorem Ipsum текстового файла ответа до 2,044 байт, сжимает ~ 979 байт.
    * **/testfile1kb.txt** -текстового файла ответа до 1,033 байт, сжимает до около 36 байтов.
    * **/ Тонкая** -ответ, выданный в качестве отдельных символов, с интервалом в 1.
* `GzipCompressionProvider`
  * `text/plain`
    * **/** -Lorem Ipsum текстового файла ответа до 2,044 байт, сжимает ~ 927 байт.
    * **/testfile1kb.txt** -текстового файла ответа до 1,033 байт, сжимает байт ~ 47.
    * **/ Тонкая** -ответ, выданный в качестве отдельных символов, с интервалом в 1.
  * `image/svg+xml`
    * **/Banner.SVG** — масштабируемый векторный рисунок (SVG) образа ответ до 9,707 байт, сжимает ~ 4,459 байт.
* `CustomCompressionProvider`<br>Показано, как реализовать поставщик сжатия для использования с по промежуточного слоя.

Если запрос содержит `Accept-Encoding` успешна сжатие заголовка и ответа, по промежуточного слоя автоматически добавляет `Vary: Accept-Encoding` в ответ заголовок. `Vary` Заголовок указывает кэши, чтобы поддерживать несколько копий ответа на основе альтернативных значений `Accept-Encoding`, поэтому оба, сжатые (Gzip или Brotli) и размер несжатой версии хранятся в кэши для систем, можно либо принять сжатый или несжатый ответ.

## <a name="use-the-sample"></a>Используйте пример

1. Запрос с помощью [Fiddler](http://www.telerik.com/fiddler), [Firebug](http://getfirebug.com/), или [Postman](https://www.getpostman.com/) к приложению без `Accept-Encoding` заголовок и Примечание полезные данные ответа, размер ответа, и заголовки ответа.
1. Добавить `Accept-Encoding: br` или `Accept-Encoding: gzip` заголовка и обратите внимание на размер сжатого ответа и заголовки ответа. Снижается размер ответа и `Content-Encoding` возникновения Brotli или по промежуточного слоя, указывающее, что сжатие с помощью Gzip, либо включен заголовок ответа. Если взглянуть на тексте ответа для Lorem Ipsum или **testfile1kb.txt** ответа, вы видите, что текст является сжатые и может быть прочитан.
1. Добавление `Accept-Encoding: mycustomcompression` заголовка и обратите внимание, заголовки ответа. `CustomCompressionProvider` Пустую реализацию, фактически не сжимать ответ, но можно создать оболочку поток сжатия для `CreateStream()` метод.
