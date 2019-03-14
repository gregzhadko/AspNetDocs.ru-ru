---
ms.openlocfilehash: d7ef9b11af8ee11e4ec84404f8cdeb0b89384a3c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57130454"
---
## <a name="forward-request-information-with-a-proxy-or-load-balancer"></a><span data-ttu-id="47f82-101">Вперед запрашивать информацию с помощью прокси-сервер или подсистему балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="47f82-101">Forward request information with a proxy or load balancer</span></span>

<span data-ttu-id="47f82-102">Если приложение развертывается за прокси-сервер или подсистемы балансировки нагрузки, некоторые данные исходного запроса может перенаправляться в приложение, в заголовках запроса.</span><span class="sxs-lookup"><span data-stu-id="47f82-102">If the app is deployed behind a proxy server or load balancer, some of the original request information might be forwarded to the app in request headers.</span></span> <span data-ttu-id="47f82-103">Эти сведения обычно включает безопасный запрос схему (`https`), узла и IP-адрес клиента.</span><span class="sxs-lookup"><span data-stu-id="47f82-103">This information usually includes the secure request scheme (`https`), host, and client IP address.</span></span> <span data-ttu-id="47f82-104">Приложения не считать эти заголовки запроса, находить и использовать данные исходного запроса автоматически.</span><span class="sxs-lookup"><span data-stu-id="47f82-104">Apps don't automatically read these request headers to discover and use the original request information.</span></span>

<span data-ttu-id="47f82-105">Схема используется в компоновки, который влияет на процесс проверки подлинности с помощью внешних поставщиков.</span><span class="sxs-lookup"><span data-stu-id="47f82-105">The scheme is used in link generation that affects the authentication flow with external providers.</span></span> <span data-ttu-id="47f82-106">Потери безопасного схемы (`https`) приводит приложение формирование неверные небезопасные перенаправления URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="47f82-106">Losing the secure scheme (`https`) results in the app generating incorrect insecure redirect URLs.</span></span>

<span data-ttu-id="47f82-107">Используйте перенаправленные заголовки по промежуточного слоя для предоставления исходных сведений запроса в приложении для обработки запроса.</span><span class="sxs-lookup"><span data-stu-id="47f82-107">Use Forwarded Headers Middleware to make the original request information available to the app for request processing.</span></span>

<span data-ttu-id="47f82-108">Дополнительные сведения см. в разделе <xref:host-and-deploy/proxy-load-balancer>.</span><span class="sxs-lookup"><span data-stu-id="47f82-108">For more information, see <xref:host-and-deploy/proxy-load-balancer>.</span></span>
