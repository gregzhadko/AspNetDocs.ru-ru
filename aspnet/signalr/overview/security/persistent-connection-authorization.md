---
uid: signalr/overview/security/persistent-connection-authorization
title: Проверка подлинности и авторизация для постоянных подключений SignalR | Документация Майкрософт
author: bradygaster
description: В этом разделе описывается, как требовать принудительной авторизации на постоянное подключение. Общие сведения об интеграции безопасности в приложении SignalR...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 7e69d3c1a18f1239142891734ba58cd2b0078f84
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65113527"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a><span data-ttu-id="1d0d1-104">Проверка подлинности и авторизация для постоянных подключений SignalR</span><span class="sxs-lookup"><span data-stu-id="1d0d1-104">Authentication and Authorization for SignalR Persistent Connections</span></span>

<span data-ttu-id="1d0d1-105">по [Флетчера Патрик](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="1d0d1-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="1d0d1-106">В этом разделе описывается, как требовать принудительной авторизации на постоянное подключение.</span><span class="sxs-lookup"><span data-stu-id="1d0d1-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="1d0d1-107">Общие сведения об интеграции безопасности в приложении SignalR, см. в разделе [Общие сведения о безопасности](introduction-to-security.md).</span><span class="sxs-lookup"><span data-stu-id="1d0d1-107">For general information about integrating security into a SignalR application, see [Introduction to Security](introduction-to-security.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="1d0d1-108">Версии программного обеспечения, используемого в этом разделе</span><span class="sxs-lookup"><span data-stu-id="1d0d1-108">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="1d0d1-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="1d0d1-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="1d0d1-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="1d0d1-110">.NET 4.5</span></span>
> - <span data-ttu-id="1d0d1-111">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="1d0d1-111">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="1d0d1-112">Предыдущие версии этого раздела</span><span class="sxs-lookup"><span data-stu-id="1d0d1-112">Previous versions of this topic</span></span>
>
> <span data-ttu-id="1d0d1-113">Сведения о более ранних версий SignalR, см. в разделе [более старых версий SignalR](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="1d0d1-113">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="1d0d1-114">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="1d0d1-114">Questions and comments</span></span>
>
> <span data-ttu-id="1d0d1-115">Оставьте свои отзывы на том, как вам понравилось, и этот учебник и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="1d0d1-115">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="1d0d1-116">Если у вас есть вопросы, которые не имеют отношения к руководству, их можно разместить [форум по ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="1d0d1-116">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="1d0d1-117">Требовать принудительной авторизации</span><span class="sxs-lookup"><span data-stu-id="1d0d1-117">Enforce authorization</span></span>

<span data-ttu-id="1d0d1-118">Для принудительного выполнения правил авторизации, при использовании [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) необходимо переопределить `AuthorizeRequest` метод.</span><span class="sxs-lookup"><span data-stu-id="1d0d1-118">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="1d0d1-119">Нельзя использовать `Authorize` атрибута с постоянные подключения.</span><span class="sxs-lookup"><span data-stu-id="1d0d1-119">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="1d0d1-120">`AuthorizeRequest` Метод вызывается инфраструктурой SignalR перед каждым запросом, чтобы убедиться, что пользователь авторизован для выполнения запрошенного действия.</span><span class="sxs-lookup"><span data-stu-id="1d0d1-120">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="1d0d1-121">`AuthorizeRequest` Метод не вызывается из клиента; вместо этого проверки подлинности пользователя через механизм стандартной проверки подлинности приложения.</span><span class="sxs-lookup"><span data-stu-id="1d0d1-121">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="1d0d1-122">В приведенном ниже примере показано, как ограничить запросы пользователям, прошедшим проверку.</span><span class="sxs-lookup"><span data-stu-id="1d0d1-122">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="1d0d1-123">Можно добавить логику настраиваемой авторизации в методе AuthorizeRequest; например проверка, принадлежит ли пользователь к определенной роли.</span><span class="sxs-lookup"><span data-stu-id="1d0d1-123">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
