---
ms.openlocfilehash: 2cd201e16cd491d0f468e8ef141b522f1694a257
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57165864"
---
<span data-ttu-id="c7775-101">**Предупреждение**: В следующем коде используется `GetTempFileName`, какие вызывает `IOException` Если превышает 65535 файлы создаются без удаления предыдущей временные файлы.</span><span class="sxs-lookup"><span data-stu-id="c7775-101">**Warning**: The following code uses `GetTempFileName`, which throws an `IOException` if more than 65535 files are created without deleting previous temporary files.</span></span> <span data-ttu-id="c7775-102">Реальное приложение должно удалить временные файлы или использовать `GetTempPath` и `GetRandomFileName` для создания имен временных файлов.</span><span class="sxs-lookup"><span data-stu-id="c7775-102">A real app should either delete temporary files or use `GetTempPath` and `GetRandomFileName` to create temporary file names.</span></span> <span data-ttu-id="c7775-103">Существует ограничение в 65 535 файлов на сервер, поэтому другое приложение на сервере может использовать максимум 65 535 файлов.</span><span class="sxs-lookup"><span data-stu-id="c7775-103">The 65535 files limit is per server, so another app on the server can use up all 65535 files.</span></span> 
