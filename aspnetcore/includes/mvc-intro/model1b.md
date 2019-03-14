---
ms.openlocfilehash: 1c342231905775938715280681ea2b4cf6ebc9bc
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047941"
---
<span data-ttu-id="9e581-101">Добавьте в класс `Movie` следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="9e581-101">Add the following properties to the `Movie` class:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Models/Movie.cs?name=snippet1)]

<span data-ttu-id="9e581-102">Класс `Movie` содержит:</span><span class="sxs-lookup"><span data-stu-id="9e581-102">The `Movie` class contains:</span></span>

* <span data-ttu-id="9e581-103">Поле `Id`, которое является обязательным для первичного ключа базы данных.</span><span class="sxs-lookup"><span data-stu-id="9e581-103">The `Id` field which is required by the database for the primary key.</span></span>
* <span data-ttu-id="9e581-104">`[DataType(DataType.Date)]`:  Атрибут [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) указывает тип данных (`Date`).</span><span class="sxs-lookup"><span data-stu-id="9e581-104">`[DataType(DataType.Date)]`:  The [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) attribute specifies the type of the data (`Date`).</span></span> <span data-ttu-id="9e581-105">С этим атрибутом:</span><span class="sxs-lookup"><span data-stu-id="9e581-105">With this attribute:</span></span>

  * <span data-ttu-id="9e581-106">пользователю не требуется вводить сведения о времени в поле даты.</span><span class="sxs-lookup"><span data-stu-id="9e581-106">The user is not required to enter time information in the date field.</span></span>
  * <span data-ttu-id="9e581-107">Отображается только дата, а не время.</span><span class="sxs-lookup"><span data-stu-id="9e581-107">Only the date is displayed, not time information.</span></span>

<span data-ttu-id="9e581-108">[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) рассматриваются в следующем руководстве.</span><span class="sxs-lookup"><span data-stu-id="9e581-108">[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) are covered in a later tutorial.</span></span>