---
title: Перенос из проверки подлинности членства ASP.NET, в удостоверение ASP.NET Core 2.0
author: isaac2004
description: Сведения о переносе существующих приложений ASP.NET с использованием проверки подлинности членства в ASP.NET Core 2.0 Identity.
ms.author: scaddie
ms.custom: mvc
ms.date: 01/10/2019
uid: migration/proper-to-2x/membership-to-core-identity
ms.openlocfilehash: 0b7001a311eeaaa78e3d52e2ec66d33ad057c381
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57054501"
---
# <a name="migrate-from-aspnet-membership-authentication-to-aspnet-core-20-identity"></a>Перенос из проверки подлинности членства ASP.NET, в удостоверение ASP.NET Core 2.0

Автор [Айзек Левин](https://isaaclevin.com) (Isaac Levin)

В этой статье показано, перенос схемы базы данных для приложений ASP.NET с использованием проверки подлинности членства в ASP.NET Core 2.0 Identity.

> [!NOTE]
> В этом документе описываются действия, необходимые для переноса схемы базы данных для приложения на основе членства ASP.NET со схемой базы данных, используемый для удостоверения ASP.NET Core. Дополнительные сведения о переходе с проверки подлинности на основе членства ASP.NET на ASP.NET Identity см. в разделе [перенести существующее приложение из членства SQL в ASP.NET Identity](/aspnet/identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity). Дополнительные сведения о ASP.NET Core Identity, см. в разделе [Общие сведения об Identity в ASP.NET Core](xref:security/authentication/identity).

## <a name="review-of-membership-schema"></a>Обзор схемы членства

До ASP.NET 2.0 разработчики были заниматься созданием весь процесс проверки подлинности и авторизации для своих приложений. В ASP.NET 2.0 появилась членства, предоставляя стандартный решение по обработке безопасности в приложениях ASP.NET. Теперь бы разработчики могли для начальной загрузки схемы в базу данных SQL Server с [aspnet_regsql.exe](https://msdn.microsoft.com/library/ms229862.aspx) команды. После выполнения этой команды, следующие таблицы были созданы в базе данных.

  ![Таблицы членства](identity/_static/membership-tables.png)

Чтобы перенести существующие приложения в удостоверение ASP.NET Core 2.0, данные в этих таблицах требует переноса таблиц, используемых новой схемы идентификации.

## <a name="aspnet-core-identity-20-schema"></a>ASP.NET Core Identity 2.0 схемы

ASP.NET Core 2.0 соответствует [удостоверений](/aspnet/identity/index) принцип, появившиеся в ASP.NET 4.5. На то, что принцип является общим, реализация между платформами, отличается, даже между версиями ASP.NET Core (см. в разделе [миграция проверки подлинности и удостоверения в ASP.NET Core 2.0](xref:migration/1x-to-2x/index)).

Самый быстрый способ просмотра схемы для удостоверения ASP.NET Core 2.0 является создание нового приложения ASP.NET Core 2.0. Выполните следующие действия в Visual Studio 2017.

1. Выберите **Файл** > **Создать** > **Проект**.
1. Создайте новый **веб-приложение ASP.NET Core** проект с именем *CoreIdentitySample*.
1. Выберите **ASP.NET Core 2.0** в раскрывающемся списке, а затем выберите **веб-приложение**. Этот шаблон создает [Razor Pages](xref:razor-pages/index) приложения. Перед нажатием кнопки **ОК**, нажмите кнопку **изменить способ проверки подлинности**.
1. Выберите **учетные записи отдельных пользователей** для идентификации шаблонов. Наконец, нажмите кнопку **ОК**, затем **ОК**. Visual Studio создает проект с помощью шаблона ASP.NET Core Identity.
1. Выберите **средства** > **диспетчер пакетов NuGet** > **консоль диспетчера пакетов** открыть **консоль диспетчера пакетов** Окно (PMC).
1. Перейдите в корневую папку проекта в PMC и запустите [Entity Framework (EF) Core](/ef/core) `Update-Database` команды.

    Удостоверение ASP.NET Core 2.0 использует EF Core для взаимодействия с базой данных, хранение данных проверки подлинности. Чтобы созданное приложение для работы должен быть базой данных для хранения этих данных. После создания нового приложения, то самый быстрый способ проверить схему в среде базы данных является создание базы данных с помощью [миграций EF Core](/ef/core/managing-schemas/migrations/). Этот процесс создает базу данных, либо локально или в другом месте, что повторяет эту схему. В документации по предыдущей Дополнительные сведения.

    Команды EF Core используйте строку подключения для базы данных, указанной в *appsettings.json*. Следующая строка подключения связанного с базой данных на *localhost* с именем *asp-net-core-identity*. В этом параметре, EF Core настроен на использование `DefaultConnection` строку подключения.

    ```json
    {
      "ConnectionStrings": {
        "DefaultConnection": "Server=localhost;Database=aspnet-core-identity;Trusted_Connection=True;MultipleActiveResultSets=true"
      }
    }
    ```
1. Выберите **представление** > **обозреватель объектов SQL Server**. Разверните узел, соответствующий имени базы данных, указанному в `ConnectionStrings:DefaultConnection` свойство *appsettings.json*.

    `Update-Database` Команда создала базы данных, указанной с помощью схемы и все данные, необходимые для инициализации приложения. На следующем рисунке изображены структуру таблицы, созданного в предыдущих шагах.

    ![Удостоверение таблиц](identity/_static/identity-tables.png)

## <a name="migrate-the-schema"></a>Перенос схемы

Существуют небольшие отличия в структуры таблиц и полей для членства и удостоверения ASP.NET Core. Шаблон значительно изменяется для проверки подлинности и авторизации с приложениями ASP.NET и ASP.NET Core. Основные объекты, которые по-прежнему используются с удостоверением *пользователей* и *ролей*. Ниже приведены таблицы сопоставления для *пользователей*, *ролей*, и *UserRoles*.

### <a name="users"></a>Users

|*Удостоверение<br>(dbo. AspNetUsers)*        ||*Членство<br>(dbo.aspnet_Users / dbo.aspnet_Membership)*||
|----------------------------------------|-----------------------------------------------------------|
|**Имя поля**                 |**Type**|**Имя поля**                                    |**Type**|
|`Id`                           |string  |`aspnet_Users.UserId`                             |string  |
|`UserName`                     |string  |`aspnet_Users.UserName`                           |string  |
|`Email`                        |string  |`aspnet_Membership.Email`                         |string  |
|`NormalizedUserName`           |string  |`aspnet_Users.LoweredUserName`                    |string  |
|`NormalizedEmail`              |string  |`aspnet_Membership.LoweredEmail`                  |string  |
|`PhoneNumber`                  |string  |`aspnet_Users.MobileAlias`                        |string  |
|`LockoutEnabled`               |bit     |`aspnet_Membership.IsLockedOut`                   |bit     |

> [!NOTE]
> Не все сопоставления полей похожи на отношения один к одному из членства в ASP.NET Core Identity. Приведенной выше таблице, используется схема по умолчанию авторизованного пользователя и сопоставляет его схемы удостоверения ASP.NET Core. Другие настраиваемые поля, которые были использованы для членства должны быть добавлены вручную. В этом сопоставлении нет отсутствует сопоставление для паролей, как требования к паролям и соли пароля не будут перемещаться между ними. **Рекомендуется оставлять пароль как null и предлагать пользователям сбрасывать свои пароли.** В ASP.NET Core Identity `LockoutEnd` следует задавать на некоторую дату в будущем, если пользователь будет заблокирован. Это показано в сценарии миграции.

### <a name="roles"></a>Роли

|*Удостоверение<br>(dbo. AspNetRoles)*        ||*Членство<br>(dbo.aspnet_Roles)*||
|----------------------------------------|-----------------------------------|
|**Имя поля**                 |**Type**|**Имя поля**   |**Type**         |
|`Id`                           |string  |`RoleId`         | string          |
|`Name`                         |string  |`RoleName`       | string          |
|`NormalizedName`               |string  |`LoweredRoleName`| string          |

### <a name="user-roles"></a>Роли пользователей

|*Identity<br>(dbo.AspNetUserRoles)*||*Членство<br>(dbo.aspnet_UsersInRoles)*||
|------------------------------------|------------------------------------------|
|**Имя поля**           |**Type**  |**Имя поля**|**Type**                   |
|`RoleId`                 |string    |`RoleId`      |string                     |
|`UserId`                 |string    |`UserId`      |string                     |

Ссылаться на предыдущем сопоставление таблиц, при создании сценария миграции для *пользователей* и *ролей*. В следующем примере предполагается, что у вас есть две базы данных на сервере базы данных. Одна база данных содержит существующую схему членства ASP.NET и данные. Другой *CoreIdentitySample* база данных была создана, выполнив действия, описанные ранее. Комментарии — это встроенные вместе для получения дополнительных сведений.

```sql
-- THIS SCRIPT NEEDS TO RUN FROM THE CONTEXT OF THE MEMBERSHIP DB
BEGIN TRANSACTION MigrateUsersAndRoles
USE aspnetdb

-- INSERT USERS
INSERT INTO CoreIdentitySample.dbo.AspNetUsers
            (Id,
             UserName,
             NormalizedUserName,
             PasswordHash,
             SecurityStamp,
             EmailConfirmed,
             PhoneNumber,
             PhoneNumberConfirmed,
             TwoFactorEnabled,
             LockoutEnd,
             LockoutEnabled,
             AccessFailedCount,
             Email,
             NormalizedEmail)
SELECT aspnet_Users.UserId,
       aspnet_Users.UserName,
       -- The NormalizedUserName value is upper case in ASP.NET Core Identity
       UPPER(aspnet_Users.UserName),
       -- Creates an empty password since passwords don't map between the 2 schemas
       '',
       /*
        The SecurityStamp token is used to verify the state of an account and 
        is subject to change at any time. It should be initialized as a new ID.
       */
       NewID(),
       /*
        EmailConfirmed is set when a new user is created and confirmed via email.
        Users must have this set during migration to reset passwords.
       */
       1,
       aspnet_Users.MobileAlias,
       CASE
         WHEN aspnet_Users.MobileAlias IS NULL THEN 0
         ELSE 1
       END,
       -- 2FA likely wasn't setup in Membership for users, so setting as false.
       0,
       CASE
         -- Setting lockout date to time in the future (1,000 years)
         WHEN aspnet_Membership.IsLockedOut = 1 THEN Dateadd(year, 1000,
                                                     Sysutcdatetime())
         ELSE NULL
       END,
       aspnet_Membership.IsLockedOut,
       /*
        AccessFailedAccount is used to track failed logins. This is stored in
        Membership in multiple columns. Setting to 0 arbitrarily.
       */
       0,
       aspnet_Membership.Email,
       -- The NormalizedEmail value is upper case in ASP.NET Core Identity
       UPPER(aspnet_Membership.Email)
FROM   aspnet_Users
       LEFT OUTER JOIN aspnet_Membership
                    ON aspnet_Membership.ApplicationId =
                       aspnet_Users.ApplicationId
                       AND aspnet_Users.UserId = aspnet_Membership.UserId
       LEFT OUTER JOIN CoreIdentitySample.dbo.AspNetUsers
                    ON aspnet_Membership.UserId = AspNetUsers.Id
WHERE  AspNetUsers.Id IS NULL

-- INSERT ROLES
INSERT INTO CoreIdentitySample.dbo.AspNetRoles(Id, Name)
SELECT RoleId, RoleName
FROM aspnet_Roles;

-- INSERT USER ROLES
INSERT INTO CoreIdentitySample.dbo.AspNetUserRoles(UserId, RoleId)
SELECT UserId, RoleId
FROM aspnet_UsersInRoles;

IF @@ERROR <> 0
  BEGIN
    ROLLBACK TRANSACTION MigrateUsersAndRoles
    RETURN
  END

COMMIT TRANSACTION MigrateUsersAndRoles
```

После завершения приведенный выше сценарий созданного ранее приложения ASP.NET Core Identity заполняется авторизованных пользователей. Пользователи должны изменить свои пароли, прежде чем войти в.

> [!NOTE]
> Если система членства пользователей с именами пользователей, не соответствует адресу электронной почты, изменения требуются для приложения, созданного ранее, чтобы решить эту проблему. Шаблон по умолчанию ожидает `UserName` и `Email` должны совпадать. Для ситуаций, в которых они отличаются, процесс входа в систему необходимо изменить, чтобы использовать `UserName` вместо `Email`.

В `PageModel` страницы входа, расположенный *Pages\Account\Login.cshtml.cs*, удалите `[EmailAddress]` из атрибута *электронной почты* свойство. Переименуйте его в *UserName*. Это требует изменения везде, где `EmailAddress` упоминается, в *представление* и *PageModel*. Результат выглядит следующим образом:

 ![Фиксированного имени входа](identity/_static/fixed-login.png)

## <a name="next-steps"></a>Следующие шаги

В этом руководстве вы узнали, как перенос пользователей из членства SQL в удостоверение ASP.NET Core 2.0. Дополнительные сведения о удостоверения ASP.NET Core см. в разделе [Общие сведения об Identity](xref:security/authentication/identity).
