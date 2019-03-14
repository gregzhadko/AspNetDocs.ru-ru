---
ms.openlocfilehash: 025a244812a50709bfd48de9f47a234a547c53e2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047421"
---
<!-- THIS INCLUDE USED BY MVC AND RP -->Добавьте в класс `Movie` следующие свойства:

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/Movie.cs?name=snippet1)]

Класс `Movie` содержит:

* Поле `ID` является обязательным для первичного ключа базы данных.
* `[DataType(DataType.Date)]`:  Атрибут [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) указывает тип данных (Date). С этим атрибутом:

  * пользователю не требуется вводить сведения о времени в поле даты.
  * Отображается только дата, а не время.

[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) рассматриваются в следующем руководстве.