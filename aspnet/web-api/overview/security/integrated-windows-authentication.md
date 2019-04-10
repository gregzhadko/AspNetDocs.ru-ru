---
uid: web-api/overview/security/integrated-windows-authentication
title: Встроенная проверка подлинности Windows | Документация Майкрософт
author: MikeWasson
description: Описывает использование встроенной проверки подлинности Windows в ASP.NET Web API.
ms.author: riande
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: ce845eb6c914321736d77e989f10344eb7596eba
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59416835"
---
# <a name="integrated-windows-authentication"></a><span data-ttu-id="5969f-103">Встроенная проверка подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="5969f-103">Integrated Windows Authentication</span></span>

<span data-ttu-id="5969f-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5969f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="5969f-105">Встроенная проверка подлинности Windows позволяет пользователям войти, используя свои учетные данные Windows, с помощью Kerberos или NTLM.</span><span class="sxs-lookup"><span data-stu-id="5969f-105">Integrated Windows authentication enables users to log in with their Windows credentials, using Kerberos or NTLM.</span></span> <span data-ttu-id="5969f-106">Клиент отправляет учетные данные в заголовке авторизации.</span><span class="sxs-lookup"><span data-stu-id="5969f-106">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="5969f-107">Проверка подлинности Windows лучше всего подходит для среды интрасети.</span><span class="sxs-lookup"><span data-stu-id="5969f-107">Windows authentication is best suited for an intranet environment.</span></span> <span data-ttu-id="5969f-108">Дополнительные сведения: [Проверка подлинности Windows](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span><span class="sxs-lookup"><span data-stu-id="5969f-108">For more information, see [Windows Authentication](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span></span>

| <span data-ttu-id="5969f-109">Преимущества</span><span class="sxs-lookup"><span data-stu-id="5969f-109">Advantages</span></span> | <span data-ttu-id="5969f-110">Недостатки</span><span class="sxs-lookup"><span data-stu-id="5969f-110">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="5969f-111">-Встроены в IIS.</span><span class="sxs-lookup"><span data-stu-id="5969f-111">- Built into IIS.</span></span> <span data-ttu-id="5969f-112">-Не отправляет учетные данные пользователя в запросе.</span><span class="sxs-lookup"><span data-stu-id="5969f-112">- Does not send the user credentials in the request.</span></span> <span data-ttu-id="5969f-113">— Если клиентский компьютер принадлежит к домену (например, приложение интрасети), пользователю не нужно вводить учетные данные.</span><span class="sxs-lookup"><span data-stu-id="5969f-113">- If the client computer belongs to the domain (for example, intranet application), the user does not need to enter credentials.</span></span> | <span data-ttu-id="5969f-114">-Не рекомендуется для Интернет-приложений.</span><span class="sxs-lookup"><span data-stu-id="5969f-114">- Not recommended for Internet applications.</span></span> <span data-ttu-id="5969f-115">— Требует поддержки Kerberos или NTLM в клиенте.</span><span class="sxs-lookup"><span data-stu-id="5969f-115">- Requires Kerberos or NTLM support in the client.</span></span> <span data-ttu-id="5969f-116">-Клиент должен находиться в домене Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5969f-116">- Client must be in the Active Directory domain.</span></span> |

> [!NOTE]
> <span data-ttu-id="5969f-117">Если приложение размещено в Azure, и у вас есть домен Active Directory на предприятии, рассмотрите возможность федерации в локальной AD с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5969f-117">If your application is hosted on Azure and you have an on-premise Active Directory domain, consider federating your on-premise AD with Azure Active Directory.</span></span> <span data-ttu-id="5969f-118">Таким образом, пользователи могут входить с использованием учетных данных на предприятии, но выполняется проверка подлинности с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5969f-118">That way, users can log in with their on-premise credentials, but the authentication is performed by Azure AD.</span></span> <span data-ttu-id="5969f-119">Дополнительные сведения см. в разделе [проверки подлинности Azure](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5969f-119">For more information, see [Azure Authentication](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span></span>


<span data-ttu-id="5969f-120">Чтобы создать приложение, использующее Windows интегрированной проверки подлинности, выберите шаблон «Приложение интрасети» в мастере проектов MVC 4.</span><span class="sxs-lookup"><span data-stu-id="5969f-120">To create an application that uses Integrated Windows authentication, select the "Intranet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="5969f-121">Этот шаблон проекта помещает следующий параметр в файле Web.config:</span><span class="sxs-lookup"><span data-stu-id="5969f-121">This project template puts the following setting in the Web.config file:</span></span>

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

<span data-ttu-id="5969f-122">На стороне клиента, проверки подлинности встроенная Windows работает с помощью любого браузера, поддерживающего [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) схему проверки подлинности, которая включает в себя большинства популярных браузеров.</span><span class="sxs-lookup"><span data-stu-id="5969f-122">On the client side, Integrated Windows authentication works with any browser that supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) authentication scheme, which includes most major browsers.</span></span> <span data-ttu-id="5969f-123">Для клиентских приложений .NET **HttpClient** класс поддерживает проверку подлинности Windows:</span><span class="sxs-lookup"><span data-stu-id="5969f-123">For .NET client applications, the **HttpClient** class supports Windows authentication:</span></span>

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

<span data-ttu-id="5969f-124">Проверка подлинности Windows является уязвимым для атак с подделкой межсайтовых.</span><span class="sxs-lookup"><span data-stu-id="5969f-124">Windows authentication is vulnerable to cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="5969f-125">См. в разделе [атак с подделкой межсайтовых запросов](preventing-cross-site-request-forgery-csrf-attacks.md).</span><span class="sxs-lookup"><span data-stu-id="5969f-125">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>
