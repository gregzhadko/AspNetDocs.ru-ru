---
title: Настройка защиты данных в ASP.NET Core
author: rick-anderson
description: Узнайте, как настроить защиту данных в ASP.NET Core.
ms.author: riande
ms.custom: mvc
ms.date: 11/13/2018
uid: security/data-protection/configuration/overview
ms.openlocfilehash: 0aef2680f48b7923579f90943846f22734f61b50
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061661"
---
# <a name="configure-aspnet-core-data-protection"></a><span data-ttu-id="99f43-103">Настройка защиты данных в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="99f43-103">Configure ASP.NET Core Data Protection</span></span>

<span data-ttu-id="99f43-104">При инициализации системы защиты данных, оно применяется [параметры по умолчанию](xref:security/data-protection/configuration/default-settings) зависимости от рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="99f43-104">When the Data Protection system is initialized, it applies [default settings](xref:security/data-protection/configuration/default-settings) based on the operational environment.</span></span> <span data-ttu-id="99f43-105">Эти параметры обычно подходят для приложений, выполняющихся на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="99f43-105">These settings are generally appropriate for apps running on a single machine.</span></span> <span data-ttu-id="99f43-106">Бывают случаи, где разработчик может потребоваться изменить параметры по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="99f43-106">There are cases where a developer may want to change the default settings:</span></span>

* <span data-ttu-id="99f43-107">Приложения распределены между несколькими компьютерами.</span><span class="sxs-lookup"><span data-stu-id="99f43-107">The app is spread across multiple machines.</span></span>
* <span data-ttu-id="99f43-108">Для обеспечения соответствия.</span><span class="sxs-lookup"><span data-stu-id="99f43-108">For compliance reasons.</span></span>

<span data-ttu-id="99f43-109">В таких случаях системы защиты данных предлагает широкие возможности настройки API.</span><span class="sxs-lookup"><span data-stu-id="99f43-109">For these scenarios, the Data Protection system offers a rich configuration API.</span></span>

> [!WARNING]
> <span data-ttu-id="99f43-110">Как и файлы конфигурации, набора ключей защиты данных должны быть защищены с помощью соответствующих разрешений.</span><span class="sxs-lookup"><span data-stu-id="99f43-110">Similar to configuration files, the data protection key ring should be protected using appropriate permissions.</span></span> <span data-ttu-id="99f43-111">Можно выбрать для шифрования ключей при хранении, но это не предотвращает злоумышленники созданием новых ключей.</span><span class="sxs-lookup"><span data-stu-id="99f43-111">You can choose to encrypt keys at rest, but this doesn't prevent attackers from creating new keys.</span></span> <span data-ttu-id="99f43-112">Следовательно это повлияет на безопасность приложения.</span><span class="sxs-lookup"><span data-stu-id="99f43-112">Consequently, your app's security is impacted.</span></span> <span data-ttu-id="99f43-113">Место хранения, настроен с защитой данных должны иметь его доступ возможен только из самого, аналогично тому, как бы Защита файлов конфигурации приложения.</span><span class="sxs-lookup"><span data-stu-id="99f43-113">The storage location configured with Data Protection should have its access limited to the app itself, similar to the way you would protect configuration files.</span></span> <span data-ttu-id="99f43-114">Например если вы решили хранить на диске вашего набора ключей, используйте разрешения файловой системы.</span><span class="sxs-lookup"><span data-stu-id="99f43-114">For example, if you choose to store your key ring on disk, use file system permissions.</span></span> <span data-ttu-id="99f43-115">Убедитесь, удостоверение, под которой запущено приложение чтения, записи и доступа к этому каталогу.</span><span class="sxs-lookup"><span data-stu-id="99f43-115">Ensure only the identity under which your web app runs has read, write, and create access to that directory.</span></span> <span data-ttu-id="99f43-116">Если вы используете хранилище таблиц Azure, веб-приложения должны иметь возможность читать, записывать и создавать новые записи в хранилище таблиц и т. д.</span><span class="sxs-lookup"><span data-stu-id="99f43-116">If you use Azure Table Storage, only the web app should have the ability to read, write, or create new entries in the table store, etc.</span></span>
>
> <span data-ttu-id="99f43-117">Метод расширения [AddDataProtection](/dotnet/api/microsoft.extensions.dependencyinjection.dataprotectionservicecollectionextensions.adddataprotection) возвращает [IDataProtectionBuilder](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotectionbuilder).</span><span class="sxs-lookup"><span data-stu-id="99f43-117">The extension method [AddDataProtection](/dotnet/api/microsoft.extensions.dependencyinjection.dataprotectionservicecollectionextensions.adddataprotection) returns an [IDataProtectionBuilder](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotectionbuilder).</span></span> <span data-ttu-id="99f43-118">`IDataProtectionBuilder` Предоставляет методы расширения, что вы можете связать вместе, чтобы настроить защиту данных.</span><span class="sxs-lookup"><span data-stu-id="99f43-118">`IDataProtectionBuilder` exposes extension methods that you can chain together to configure Data Protection options.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="protectkeyswithazurekeyvault"></a><span data-ttu-id="99f43-119">ProtectKeysWithAzureKeyVault</span><span class="sxs-lookup"><span data-stu-id="99f43-119">ProtectKeysWithAzureKeyVault</span></span>

<span data-ttu-id="99f43-120">Для хранения ключей в [Azure Key Vault](https://azure.microsoft.com/services/key-vault/), настройки системы с [ProtectKeysWithAzureKeyVault](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault) в `Startup` класса:</span><span class="sxs-lookup"><span data-stu-id="99f43-120">To store keys in [Azure Key Vault](https://azure.microsoft.com/services/key-vault/), configure the system with [ProtectKeysWithAzureKeyVault](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault) in the `Startup` class:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToAzureBlobStorage(new Uri("<blobUriWithSasToken>"))
        .ProtectKeysWithAzureKeyVault("<keyIdentifier>", "<clientId>", "<clientSecret>");
}
```

<span data-ttu-id="99f43-121">Задать место хранения набора ключей (например, [PersistKeysToAzureBlobStorage](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.persistkeystoazureblobstorage)).</span><span class="sxs-lookup"><span data-stu-id="99f43-121">Set the key ring storage location (for example, [PersistKeysToAzureBlobStorage](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.persistkeystoazureblobstorage)).</span></span> <span data-ttu-id="99f43-122">Необходимо задать расположение, так как вызов `ProtectKeysWithAzureKeyVault` реализует [IXmlEncryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.xmlencryption.ixmlencryptor) , отключает параметры защиты автоматические данные, включая место хранения набора ключей.</span><span class="sxs-lookup"><span data-stu-id="99f43-122">The location must be set because calling `ProtectKeysWithAzureKeyVault` implements an [IXmlEncryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.xmlencryption.ixmlencryptor) that disables automatic data protection settings, including the key ring storage location.</span></span> <span data-ttu-id="99f43-123">Предыдущий пример использует хранилище BLOB-объектов для хранения набора ключей.</span><span class="sxs-lookup"><span data-stu-id="99f43-123">The preceding example uses Azure Blob Storage to persist the key ring.</span></span> <span data-ttu-id="99f43-124">Дополнительные сведения см. в разделе [поставщики хранилища ключей: Azure и Redis](xref:security/data-protection/implementation/key-storage-providers#azure-and-redis).</span><span class="sxs-lookup"><span data-stu-id="99f43-124">For more information, see [Key storage providers: Azure and Redis](xref:security/data-protection/implementation/key-storage-providers#azure-and-redis).</span></span> <span data-ttu-id="99f43-125">Также можно сохранить локально с помощью набора ключей [PersistKeysToFileSystem](xref:security/data-protection/implementation/key-storage-providers#file-system).</span><span class="sxs-lookup"><span data-stu-id="99f43-125">You can also persist the key ring locally with [PersistKeysToFileSystem](xref:security/data-protection/implementation/key-storage-providers#file-system).</span></span>

<span data-ttu-id="99f43-126">`keyIdentifier` Является идентификатор ключа хранилища ключей, используемый для шифрования ключа (например, `https://contosokeyvault.vault.azure.net/keys/dataprotection/`).</span><span class="sxs-lookup"><span data-stu-id="99f43-126">The `keyIdentifier` is the key vault key identifier used for key encryption (for example, `https://contosokeyvault.vault.azure.net/keys/dataprotection/`).</span></span>

<span data-ttu-id="99f43-127">`ProtectKeysWithAzureKeyVault` перегрузки:</span><span class="sxs-lookup"><span data-stu-id="99f43-127">`ProtectKeysWithAzureKeyVault` overloads:</span></span>

* <span data-ttu-id="99f43-128">[ProtectKeysWithAzureKeyVault (IDataProtectionBuilder KeyVaultClient, String)](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_Microsoft_Azure_KeyVault_KeyVaultClient_System_String_) позволяет использовать [KeyVaultClient](/dotnet/api/microsoft.azure.keyvault.keyvaultclient) системы защиты данных для использования хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="99f43-128">[ProtectKeysWithAzureKeyVault(IDataProtectionBuilder, KeyVaultClient, String)](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_Microsoft_Azure_KeyVault_KeyVaultClient_System_String_) permits the use of a [KeyVaultClient](/dotnet/api/microsoft.azure.keyvault.keyvaultclient) to enable the data protection system to use the key vault.</span></span>
* <span data-ttu-id="99f43-129">[ProtectKeysWithAzureKeyVault (IDataProtectionBuilder, строка, строка, X509Certificate2)](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_System_String_System_Security_Cryptography_X509Certificates_X509Certificate2_) позволяет использовать `ClientId` и [X509Certificate](/dotnet/api/system.security.cryptography.x509certificates.x509certificate2) системы защиты данных для использования хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="99f43-129">[ProtectKeysWithAzureKeyVault(IDataProtectionBuilder, String, String, X509Certificate2)](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_System_String_System_Security_Cryptography_X509Certificates_X509Certificate2_) permits the use of a `ClientId` and [X509Certificate](/dotnet/api/system.security.cryptography.x509certificates.x509certificate2) to enable the data protection system to use the key vault.</span></span>
* <span data-ttu-id="99f43-130">[ProtectKeysWithAzureKeyVault (IDataProtectionBuilder, строки, String, String)](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_System_String_System_String_) позволяет использовать `ClientId` и `ClientSecret` для включения система защиты данных для использования хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="99f43-130">[ProtectKeysWithAzureKeyVault(IDataProtectionBuilder, String, String, String)](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_System_String_System_String_) permits the use of a `ClientId` and `ClientSecret` to enable the data protection system to use the key vault.</span></span>

::: moniker-end

## <a name="persistkeystofilesystem"></a><span data-ttu-id="99f43-131">PersistKeysToFileSystem</span><span class="sxs-lookup"><span data-stu-id="99f43-131">PersistKeysToFileSystem</span></span>

<span data-ttu-id="99f43-132">Для хранения ключей UNC-ресурсе, а не в *% LOCALAPPDATA %* расположение по умолчанию, настроить систему с [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem):</span><span class="sxs-lookup"><span data-stu-id="99f43-132">To store keys on a UNC share instead of at the *%LOCALAPPDATA%* default location, configure the system with [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem):</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\directory\"));
}
```

> [!WARNING]
> <span data-ttu-id="99f43-133">При изменении ключа постоянном расположении, система шифрует больше не будет автоматически ключей при хранении, так как он не знает, является ли DPAPI соответствующего механизма шифрования.</span><span class="sxs-lookup"><span data-stu-id="99f43-133">If you change the key persistence location, the system no longer automatically encrypts keys at rest, since it doesn't know whether DPAPI is an appropriate encryption mechanism.</span></span>

## <a name="protectkeyswith"></a><span data-ttu-id="99f43-134">ProtectKeysWith\*</span><span class="sxs-lookup"><span data-stu-id="99f43-134">ProtectKeysWith\*</span></span>

<span data-ttu-id="99f43-135">Можно настроить систему для защиты неактивных ключей можно вызвать любую из [ProtectKeysWith\* ](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions) интерфейсов API настройки.</span><span class="sxs-lookup"><span data-stu-id="99f43-135">You can configure the system to protect keys at rest by calling any of the [ProtectKeysWith\*](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions) configuration APIs.</span></span> <span data-ttu-id="99f43-136">Рассмотрим пример ниже, в котором хранятся ключи на общем ресурсе UNC и шифрует эти ключи хранятся с конкретным сертификатом X.509:</span><span class="sxs-lookup"><span data-stu-id="99f43-136">Consider the example below, which stores keys on a UNC share and encrypts those keys at rest with a specific X.509 certificate:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\directory\"))
        .ProtectKeysWithCertificate("thumbprint");
}
```

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="99f43-137">В ASP.NET Core 2.1 или более поздней версии, вы можете предоставить [X509Certificate2](/dotnet/api/system.security.cryptography.x509certificates.x509certificate2) для [ProtectKeysWithCertificate](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.protectkeyswithcertificate), такие как сертификат, загруженная из файла:</span><span class="sxs-lookup"><span data-stu-id="99f43-137">In ASP.NET Core 2.1 or later, you can provide an [X509Certificate2](/dotnet/api/system.security.cryptography.x509certificates.x509certificate2) to [ProtectKeysWithCertificate](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.protectkeyswithcertificate), such as a certificate loaded from a file:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\directory\"))
        .ProtectKeysWithCertificate(
            new X509Certificate2("certificate.pfx", "password"));
}
```

::: moniker-end

<span data-ttu-id="99f43-138">См. в разделе [ключ шифрования неактивных](xref:security/data-protection/implementation/key-encryption-at-rest) Дополнительные примеры и обсуждения на механизмы встроенного ключа шифрования.</span><span class="sxs-lookup"><span data-stu-id="99f43-138">See [Key Encryption At Rest](xref:security/data-protection/implementation/key-encryption-at-rest) for more examples and discussion on the built-in key encryption mechanisms.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="unprotectkeyswithanycertificate"></a><span data-ttu-id="99f43-139">UnprotectKeysWithAnyCertificate</span><span class="sxs-lookup"><span data-stu-id="99f43-139">UnprotectKeysWithAnyCertificate</span></span>

<span data-ttu-id="99f43-140">В ASP.NET Core 2.1 или более поздней версии, могут обеспечивать циркуляцию сертификатов и расшифровки ключей при хранении, используя массив [X509Certificate2](/dotnet/api/system.security.cryptography.x509certificates.x509certificate2) сертификаты с [UnprotectKeysWithAnyCertificate](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.unprotectkeyswithanycertificate):</span><span class="sxs-lookup"><span data-stu-id="99f43-140">In ASP.NET Core 2.1 or later, you can rotate certificates and decrypt keys at rest using an array of [X509Certificate2](/dotnet/api/system.security.cryptography.x509certificates.x509certificate2) certificates with [UnprotectKeysWithAnyCertificate](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.unprotectkeyswithanycertificate):</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\directory\"))
        .ProtectKeysWithCertificate(
            new X509Certificate2("certificate.pfx", "password"));
        .UnprotectKeysWithAnyCertificate(
            new X509Certificate2("certificate_old_1.pfx", "password_1"),
            new X509Certificate2("certificate_old_2.pfx", "password_2"));
}
```

::: moniker-end

## <a name="setdefaultkeylifetime"></a><span data-ttu-id="99f43-141">SetDefaultKeyLifetime</span><span class="sxs-lookup"><span data-stu-id="99f43-141">SetDefaultKeyLifetime</span></span>

<span data-ttu-id="99f43-142">Чтобы настроить систему для использования ключа времени существования 14 дней вместо значения по умолчанию 90 дней, используйте [SetDefaultKeyLifetime](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setdefaultkeylifetime):</span><span class="sxs-lookup"><span data-stu-id="99f43-142">To configure the system to use a key lifetime of 14 days instead of the default 90 days, use [SetDefaultKeyLifetime](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setdefaultkeylifetime):</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .SetDefaultKeyLifetime(TimeSpan.FromDays(14));
}
```

## <a name="setapplicationname"></a><span data-ttu-id="99f43-143">SetApplicationName</span><span class="sxs-lookup"><span data-stu-id="99f43-143">SetApplicationName</span></span>

<span data-ttu-id="99f43-144">По умолчанию система защиты данных изолирует приложений друг от друга в зависимости от их содержимого корневого пути, даже если они совместно используют тот же репозиторий физического ключа.</span><span class="sxs-lookup"><span data-stu-id="99f43-144">By default, the Data Protection system isolates apps from one another based on their content root paths, even if they're sharing the same physical key repository.</span></span> <span data-ttu-id="99f43-145">Это предотвращает основные сведения о других защищенных полезных данных приложения.</span><span class="sxs-lookup"><span data-stu-id="99f43-145">This prevents the apps from understanding each other's protected payloads.</span></span>

<span data-ttu-id="99f43-146">Совместное использование защищенных полезных данных между приложениями:</span><span class="sxs-lookup"><span data-stu-id="99f43-146">To share protected payloads among apps:</span></span>

* <span data-ttu-id="99f43-147">Настройка <xref:Microsoft.AspNetCore.DataProtection.DataProtectionBuilderExtensions.SetApplicationName*> в каждом приложении, с тем же значением.</span><span class="sxs-lookup"><span data-stu-id="99f43-147">Configure <xref:Microsoft.AspNetCore.DataProtection.DataProtectionBuilderExtensions.SetApplicationName*> in each app with the same value.</span></span>
* <span data-ttu-id="99f43-148">Используют ту же версию API защиты данных стека между этими приложениями.</span><span class="sxs-lookup"><span data-stu-id="99f43-148">Use the same version of the Data Protection API stack across the apps.</span></span> <span data-ttu-id="99f43-149">Выполните **либо** из следующих в файлах проектов приложений:</span><span class="sxs-lookup"><span data-stu-id="99f43-149">Perform **either** of the following in the apps' project files:</span></span>
  * <span data-ttu-id="99f43-150">Ссылаться на той же версии общей платформы, с помощью [метапакет Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app).</span><span class="sxs-lookup"><span data-stu-id="99f43-150">Reference the same shared framework version via the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>
  * <span data-ttu-id="99f43-151">Ссылаются на тот же [защиты данных пакета](xref:security/data-protection/introduction#package-layout) версии.</span><span class="sxs-lookup"><span data-stu-id="99f43-151">Reference the same [Data Protection package](xref:security/data-protection/introduction#package-layout) version.</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .SetApplicationName("shared app name");
}
```

## <a name="disableautomatickeygeneration"></a><span data-ttu-id="99f43-152">DisableAutomaticKeyGeneration</span><span class="sxs-lookup"><span data-stu-id="99f43-152">DisableAutomaticKeyGeneration</span></span>

<span data-ttu-id="99f43-153">Возможно, сценарий, где вы не хотите приложению автоматически менять ключи, (создание новых ключей), так как они подходят истечения срока действия.</span><span class="sxs-lookup"><span data-stu-id="99f43-153">You may have a scenario where you don't want an app to automatically roll keys (create new keys) as they approach expiration.</span></span> <span data-ttu-id="99f43-154">Примером этого может быть приложения, в связи первичного и вторичного, где только основное приложение отвечает за управление ключами задач и дополнительный приложения просто доступное только для чтения представление набора ключей.</span><span class="sxs-lookup"><span data-stu-id="99f43-154">One example of this might be apps set up in a primary/secondary relationship, where only the primary app is responsible for key management concerns and secondary apps simply have a read-only view of the key ring.</span></span> <span data-ttu-id="99f43-155">Вторичный приложения можно настроить необходимо рассматривать набора ключей только для чтения, настройки системы с [DisableAutomaticKeyGeneration](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.disableautomatickeygeneration):</span><span class="sxs-lookup"><span data-stu-id="99f43-155">The secondary apps can be configured to treat the key ring as read-only by configuring the system with [DisableAutomaticKeyGeneration](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.disableautomatickeygeneration):</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .DisableAutomaticKeyGeneration();
}
```

## <a name="per-application-isolation"></a><span data-ttu-id="99f43-156">Изоляция на уровне приложения</span><span class="sxs-lookup"><span data-stu-id="99f43-156">Per-application isolation</span></span>

<span data-ttu-id="99f43-157">Когда система защиты данных предоставляется узлом ASP.NET Core, она автоматически изолирует приложений друг от друга, даже если эти приложения выполняются под одной учетной записи рабочего процесса и при использовании же материала главного ключа.</span><span class="sxs-lookup"><span data-stu-id="99f43-157">When the Data Protection system is provided by an ASP.NET Core host, it automatically isolates apps from one another, even if those apps are running under the same worker process account and are using the same master keying material.</span></span> <span data-ttu-id="99f43-158">Это отчасти напоминает модификатора IsolateApps из System.Web  **\<machineKey >** элемент.</span><span class="sxs-lookup"><span data-stu-id="99f43-158">This is somewhat similar to the IsolateApps modifier from System.Web's **\<machineKey>** element.</span></span>

<span data-ttu-id="99f43-159">Механизм изоляции работает путем оценки каждого приложения на локальном компьютере как уникальный клиент, таким образом [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector) административного доступа для любого приложения автоматически включает в себя идентификатор приложения в качестве дискриминатора.</span><span class="sxs-lookup"><span data-stu-id="99f43-159">The isolation mechanism works by considering each app on the local machine as a unique tenant, thus the [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector) rooted for any given app automatically includes the app ID as a discriminator.</span></span> <span data-ttu-id="99f43-160">Уникальный идентификатор приложения берутся из одного из двух мест:</span><span class="sxs-lookup"><span data-stu-id="99f43-160">The app's unique ID comes from one of two places:</span></span>

1. <span data-ttu-id="99f43-161">Если приложение размещается в службах IIS, уникальный идентификатор — это путь конфигурации приложения.</span><span class="sxs-lookup"><span data-stu-id="99f43-161">If the app is hosted in IIS, the unique identifier is the app's configuration path.</span></span> <span data-ttu-id="99f43-162">Если приложение развертывается в среде веб-фермы, это значение должно быть стабильная, при условии, что в средах службы IIS настраиваются сходным образом на всех компьютерах веб-фермы.</span><span class="sxs-lookup"><span data-stu-id="99f43-162">If an app is deployed in a web farm environment, this value should be stable assuming that the IIS environments are configured similarly across all machines in the web farm.</span></span>

2. <span data-ttu-id="99f43-163">Если приложение не размещено в службах IIS, уникальный идентификатор — это физический путь приложения.</span><span class="sxs-lookup"><span data-stu-id="99f43-163">If the app isn't hosted in IIS, the unique identifier is the physical path of the app.</span></span>

<span data-ttu-id="99f43-164">Уникальный идентификатор позволяет избежать простоев в случае сброса &mdash; как отдельные приложения и самой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="99f43-164">The unique identifier is designed to survive resets &mdash; both of the individual app and of the machine itself.</span></span>

<span data-ttu-id="99f43-165">Этот механизм изоляции предполагается, что приложения не являются вредоносными.</span><span class="sxs-lookup"><span data-stu-id="99f43-165">This isolation mechanism assumes that the apps are not malicious.</span></span> <span data-ttu-id="99f43-166">Вредоносные приложения всегда может повлиять на любое другое приложение, под одной учетной записи рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="99f43-166">A malicious app can always impact any other app running under the same worker process account.</span></span> <span data-ttu-id="99f43-167">В общей среде размещения, когда приложения являются взаимно без доверия поставщика услуг размещения принять меры для обеспечения изоляции на уровне операционной системы между приложениями, включая Отделение приложений основного ключа хранилища.</span><span class="sxs-lookup"><span data-stu-id="99f43-167">In a shared hosting environment where apps are mutually untrusted, the hosting provider should take steps to ensure OS-level isolation between apps, including separating the apps' underlying key repositories.</span></span>

<span data-ttu-id="99f43-168">Если система защиты данных не предоставляется для узла ASP.NET Core (например, в том случае, если необходимо создать его с помощью `DataProtectionProvider` конкретный тип) изоляция приложений отключена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="99f43-168">If the Data Protection system isn't provided by an ASP.NET Core host (for example, if you instantiate it via the `DataProtectionProvider` concrete type) app isolation is disabled by default.</span></span> <span data-ttu-id="99f43-169">При отключении изоляции приложений, все приложения, с тем же материала ключа, могут использовать полезные данные до тех пор, пока они предоставляют соответствующие [целей](xref:security/data-protection/consumer-apis/purpose-strings).</span><span class="sxs-lookup"><span data-stu-id="99f43-169">When app isolation is disabled, all apps backed by the same keying material can share payloads as long as they provide the appropriate [purposes](xref:security/data-protection/consumer-apis/purpose-strings).</span></span> <span data-ttu-id="99f43-170">Чтобы обеспечить изоляцию приложения в этой среде, вызовите [SetApplicationName](#setapplicationname) метод конфигурации объекта и введите уникальное имя для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="99f43-170">To provide app isolation in this environment, call the [SetApplicationName](#setapplicationname) method on the configuration object and provide a unique name for each app.</span></span>

## <a name="changing-algorithms-with-usecryptographicalgorithms"></a><span data-ttu-id="99f43-171">Изменение алгоритмов с UseCryptographicAlgorithms</span><span class="sxs-lookup"><span data-stu-id="99f43-171">Changing algorithms with UseCryptographicAlgorithms</span></span>

<span data-ttu-id="99f43-172">В стеке защиты данных можно изменить алгоритм по умолчанию, используемые вновь созданные ключи.</span><span class="sxs-lookup"><span data-stu-id="99f43-172">The Data Protection stack allows you to change the default algorithm used by newly-generated keys.</span></span> <span data-ttu-id="99f43-173">Самый простой способ сделать это является вызов [UseCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecryptographicalgorithms) из обратного вызова конфигурации:</span><span class="sxs-lookup"><span data-stu-id="99f43-173">The simplest way to do this is to call [UseCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecryptographicalgorithms) from the configuration callback:</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
services.AddDataProtection()
    .UseCryptographicAlgorithms(
        new AuthenticatedEncryptorConfiguration()
    {
        EncryptionAlgorithm = EncryptionAlgorithm.AES_256_CBC,
        ValidationAlgorithm = ValidationAlgorithm.HMACSHA256
    });
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
services.AddDataProtection()
    .UseCryptographicAlgorithms(
        new AuthenticatedEncryptionSettings()
    {
        EncryptionAlgorithm = EncryptionAlgorithm.AES_256_CBC,
        ValidationAlgorithm = ValidationAlgorithm.HMACSHA256
    });
```

::: moniker-end

<span data-ttu-id="99f43-174">По умолчанию EncryptionAlgorithm AES-256-CBC, а значение по умолчанию ValidationAlgorithm — HMACSHA256.</span><span class="sxs-lookup"><span data-stu-id="99f43-174">The default EncryptionAlgorithm is AES-256-CBC, and the default ValidationAlgorithm is HMACSHA256.</span></span> <span data-ttu-id="99f43-175">Политика по умолчанию можно задать с системным администратором через [политики на уровне компьютера](xref:security/data-protection/configuration/machine-wide-policy), но явный вызов `UseCryptographicAlgorithms` переопределяет политику по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="99f43-175">The default policy can be set by a system administrator via a [machine-wide policy](xref:security/data-protection/configuration/machine-wide-policy), but an explicit call to `UseCryptographicAlgorithms` overrides the default policy.</span></span>

<span data-ttu-id="99f43-176">Вызов `UseCryptographicAlgorithms` можно указать нужный алгоритм из предопределенного списка встроенных.</span><span class="sxs-lookup"><span data-stu-id="99f43-176">Calling `UseCryptographicAlgorithms` allows you to specify the desired algorithm from a predefined built-in list.</span></span> <span data-ttu-id="99f43-177">Не нужно беспокоиться о реализации этого алгоритма.</span><span class="sxs-lookup"><span data-stu-id="99f43-177">You don't need to worry about the implementation of the algorithm.</span></span> <span data-ttu-id="99f43-178">В сценарии выше система защиты данных пытается использовать реализацию CNG алгоритма AES, если под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="99f43-178">In the scenario above, the Data Protection system attempts to use the CNG implementation of AES if running on Windows.</span></span> <span data-ttu-id="99f43-179">В противном случае она возвращается к управляемой [System.Security.Cryptography.Aes](/dotnet/api/system.security.cryptography.aes) класса.</span><span class="sxs-lookup"><span data-stu-id="99f43-179">Otherwise, it falls back to the managed [System.Security.Cryptography.Aes](/dotnet/api/system.security.cryptography.aes) class.</span></span>

<span data-ttu-id="99f43-180">Можно вручную указать реализацию через вызов [UseCustomCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecustomcryptographicalgorithms).</span><span class="sxs-lookup"><span data-stu-id="99f43-180">You can manually specify an implementation via a call to [UseCustomCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecustomcryptographicalgorithms).</span></span>

> [!TIP]
> <span data-ttu-id="99f43-181">Изменение алгоритмов не влияет на существующие ключи в связку ключей.</span><span class="sxs-lookup"><span data-stu-id="99f43-181">Changing algorithms doesn't affect existing keys in the key ring.</span></span> <span data-ttu-id="99f43-182">Он влияет только на вновь созданные ключи.</span><span class="sxs-lookup"><span data-stu-id="99f43-182">It only affects newly-generated keys.</span></span>

### <a name="specifying-custom-managed-algorithms"></a><span data-ttu-id="99f43-183">Указание пользовательских управляемых алгоритмов</span><span class="sxs-lookup"><span data-stu-id="99f43-183">Specifying custom managed algorithms</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="99f43-184">Чтобы указать пользовательские управляемые алгоритмы, создайте [ManagedAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.managedauthenticatedencryptorconfiguration) экземпляр, который указывает типы реализации:</span><span class="sxs-lookup"><span data-stu-id="99f43-184">To specify custom managed algorithms, create a [ManagedAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.managedauthenticatedencryptorconfiguration) instance that points to the implementation types:</span></span>

```csharp
serviceCollection.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new ManagedAuthenticatedEncryptorConfiguration()
    {
        // A type that subclasses SymmetricAlgorithm
        EncryptionAlgorithmType = typeof(Aes),

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // A type that subclasses KeyedHashAlgorithm
        ValidationAlgorithmType = typeof(HMACSHA256)
    });
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="99f43-185">Чтобы указать пользовательские управляемые алгоритмы, создайте [ManagedAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.managedauthenticatedencryptionsettings) экземпляр, который указывает типы реализации:</span><span class="sxs-lookup"><span data-stu-id="99f43-185">To specify custom managed algorithms, create a [ManagedAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.managedauthenticatedencryptionsettings) instance that points to the implementation types:</span></span>

```csharp
serviceCollection.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new ManagedAuthenticatedEncryptionSettings()
    {
        // A type that subclasses SymmetricAlgorithm
        EncryptionAlgorithmType = typeof(Aes),

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // A type that subclasses KeyedHashAlgorithm
        ValidationAlgorithmType = typeof(HMACSHA256)
    });
```

::: moniker-end

<span data-ttu-id="99f43-186">Обычно \*тип свойства должен указывать на конкретный, допускающий создание экземпляров (через открытый конструктор без параметров) реализации [SymmetricAlgorithm](/dotnet/api/system.security.cryptography.symmetricalgorithm) и [KeyedHashAlgorithm](/dotnet/api/system.security.cryptography.keyedhashalgorithm), хотя Специальные случаи системы некоторые значения, такие как `typeof(Aes)` для удобства.</span><span class="sxs-lookup"><span data-stu-id="99f43-186">Generally the \*Type properties must point to concrete, instantiable (via a public parameterless ctor) implementations of [SymmetricAlgorithm](/dotnet/api/system.security.cryptography.symmetricalgorithm) and [KeyedHashAlgorithm](/dotnet/api/system.security.cryptography.keyedhashalgorithm), though the system special-cases some values like `typeof(Aes)` for convenience.</span></span>

> [!NOTE]
> <span data-ttu-id="99f43-187">SymmetricAlgorithm должен иметь длину ключа 128 бит ≥ и размер блока в ≥ 64 бита, и он должен поддерживать шифрование CBC режим заполнения PKCS #7.</span><span class="sxs-lookup"><span data-stu-id="99f43-187">The SymmetricAlgorithm must have a key length of ≥ 128 bits and a block size of ≥ 64 bits, and it must support CBC-mode encryption with PKCS #7 padding.</span></span> <span data-ttu-id="99f43-188">KeyedHashAlgorithm должен иметь размер хэш-кода > = 128 бит, и он должен поддерживать ключи равна длине дайджест хэш-алгоритма и длины.</span><span class="sxs-lookup"><span data-stu-id="99f43-188">The KeyedHashAlgorithm must have a digest size of >= 128 bits, and it must support keys of length equal to the hash algorithm's digest length.</span></span> <span data-ttu-id="99f43-189">KeyedHashAlgorithm не строго обязательно должны быть HMAC.</span><span class="sxs-lookup"><span data-stu-id="99f43-189">The KeyedHashAlgorithm isn't strictly required to be HMAC.</span></span>

### <a name="specifying-custom-windows-cng-algorithms"></a><span data-ttu-id="99f43-190">Указание пользовательские алгоритмы Windows CNG</span><span class="sxs-lookup"><span data-stu-id="99f43-190">Specifying custom Windows CNG algorithms</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="99f43-191">Чтобы задать пользовательский алгоритм Windows CNG с помощью шифрования в режиме CBC с проверкой HMAC, создайте [CngCbcAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration) экземпляр, содержащий данные алгоритма:</span><span class="sxs-lookup"><span data-stu-id="99f43-191">To specify a custom Windows CNG algorithm using CBC-mode encryption with HMAC validation, create a [CngCbcAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration) instance that contains the algorithmic information:</span></span>

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngCbcAuthenticatedEncryptorConfiguration()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // Passed to BCryptOpenAlgorithmProvider
        HashAlgorithm = "SHA256",
        HashAlgorithmProvider = null
    });
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="99f43-192">Чтобы задать пользовательский алгоритм Windows CNG с помощью шифрования в режиме CBC с проверкой HMAC, создайте [CngCbcAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cngcbcauthenticatedencryptionsettings) экземпляр, содержащий данные алгоритма:</span><span class="sxs-lookup"><span data-stu-id="99f43-192">To specify a custom Windows CNG algorithm using CBC-mode encryption with HMAC validation, create a [CngCbcAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cngcbcauthenticatedencryptionsettings) instance that contains the algorithmic information:</span></span>

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngCbcAuthenticatedEncryptionSettings()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // Passed to BCryptOpenAlgorithmProvider
        HashAlgorithm = "SHA256",
        HashAlgorithmProvider = null
    });
```

::: moniker-end

> [!NOTE]
> <span data-ttu-id="99f43-193">Алгоритм симметричного блочного шифрования должен иметь длину ключа > = 128 бит, размер блока > = 64 бита, и он должен поддерживать шифрование CBC режим заполнения PKCS #7.</span><span class="sxs-lookup"><span data-stu-id="99f43-193">The symmetric block cipher algorithm must have a key length of >= 128 bits, a block size of >= 64 bits, and it must support CBC-mode encryption with PKCS #7 padding.</span></span> <span data-ttu-id="99f43-194">Хэш-алгоритм, должен иметь размер хэш-кода из > 128 бит и должен поддерживать, открытого в BCRYPT\_ALG\_ОБРАБАТЫВАТЬ\_HMAC\_флаг ФЛАГ.</span><span class="sxs-lookup"><span data-stu-id="99f43-194">The hash algorithm must have a digest size of >= 128 bits and must support being opened with the BCRYPT\_ALG\_HANDLE\_HMAC\_FLAG flag.</span></span> <span data-ttu-id="99f43-195">\*Поставщика свойства можно задать значение null, чтобы использовать поставщика по умолчанию для указанного алгоритма.</span><span class="sxs-lookup"><span data-stu-id="99f43-195">The \*Provider properties can be set to null to use the default provider for the specified algorithm.</span></span> <span data-ttu-id="99f43-196">См. в разделе [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="99f43-196">See the [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) documentation for more information.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="99f43-197">Чтобы задать пользовательский алгоритм Windows CNG с помощью счетчиков Galois режим шифрования с помощью проверки, создайте [CngGcmAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cnggcmauthenticatedencryptorconfiguration) экземпляр, содержащий данные алгоритма:</span><span class="sxs-lookup"><span data-stu-id="99f43-197">To specify a custom Windows CNG algorithm using Galois/Counter Mode encryption with validation, create a [CngGcmAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cnggcmauthenticatedencryptorconfiguration) instance that contains the algorithmic information:</span></span>

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngGcmAuthenticatedEncryptorConfiguration()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256
    });
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="99f43-198">Чтобы задать пользовательский алгоритм Windows CNG с помощью счетчиков Galois режим шифрования с помощью проверки, создайте [CngGcmAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cnggcmauthenticatedencryptionsettings) экземпляр, содержащий данные алгоритма:</span><span class="sxs-lookup"><span data-stu-id="99f43-198">To specify a custom Windows CNG algorithm using Galois/Counter Mode encryption with validation, create a [CngGcmAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cnggcmauthenticatedencryptionsettings) instance that contains the algorithmic information:</span></span>

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngGcmAuthenticatedEncryptionSettings()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256
    });
```

::: moniker-end

> [!NOTE]
> <span data-ttu-id="99f43-199">Алгоритм симметричного блочного шифрования должен иметь длину ключа > = 128 бит, размер блока в точности 128 бит, и он должен поддерживать шифрование GCM.</span><span class="sxs-lookup"><span data-stu-id="99f43-199">The symmetric block cipher algorithm must have a key length of >= 128 bits, a block size of exactly 128 bits, and it must support GCM encryption.</span></span> <span data-ttu-id="99f43-200">Можно задать [EncryptionAlgorithmProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration.encryptionalgorithmprovider) свойство значение null, чтобы использовать поставщика по умолчанию для указанного алгоритма.</span><span class="sxs-lookup"><span data-stu-id="99f43-200">You can set the [EncryptionAlgorithmProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration.encryptionalgorithmprovider) property to null to use the default provider for the specified algorithm.</span></span> <span data-ttu-id="99f43-201">См. в разделе [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="99f43-201">See the [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) documentation for more information.</span></span>

### <a name="specifying-other-custom-algorithms"></a><span data-ttu-id="99f43-202">Указание другие пользовательские алгоритмы</span><span class="sxs-lookup"><span data-stu-id="99f43-202">Specifying other custom algorithms</span></span>

<span data-ttu-id="99f43-203">Хотя не представлен как первоклассную API, система защиты данных достаточно расширяемым для того, чтобы обеспечить возможность указания практически любой тип алгоритма.</span><span class="sxs-lookup"><span data-stu-id="99f43-203">Though not exposed as a first-class API, the Data Protection system is extensible enough to allow specifying almost any kind of algorithm.</span></span> <span data-ttu-id="99f43-204">Например можно сохранить все ключи, содержащиеся в модуле оборудования безопасности (HSM) и предоставить пользовательскую реализацию основные процедуры шифрования и расшифровки.</span><span class="sxs-lookup"><span data-stu-id="99f43-204">For example, it's possible to keep all keys contained within a Hardware Security Module (HSM) and to provide a custom implementation of the core encryption and decryption routines.</span></span> <span data-ttu-id="99f43-205">См. в разделе [IAuthenticatedEncryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.iauthenticatedencryptor) в [основы расширяемости шифрования](xref:security/data-protection/extensibility/core-crypto) Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="99f43-205">See [IAuthenticatedEncryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.iauthenticatedencryptor) in [Core cryptography extensibility](xref:security/data-protection/extensibility/core-crypto) for more information.</span></span>

## <a name="persisting-keys-when-hosting-in-a-docker-container"></a><span data-ttu-id="99f43-206">Сохранение ключей при размещении в контейнере Docker</span><span class="sxs-lookup"><span data-stu-id="99f43-206">Persisting keys when hosting in a Docker container</span></span>

<span data-ttu-id="99f43-207">При размещении в [Docker](/dotnet/standard/microservices-architecture/container-docker-introduction/) контейнера, ключи следует хранить в одном:</span><span class="sxs-lookup"><span data-stu-id="99f43-207">When hosting in a [Docker](/dotnet/standard/microservices-architecture/container-docker-introduction/) container, keys should be maintained in either:</span></span>

* <span data-ttu-id="99f43-208">Папка, — это том Docker, который сохраняется вне пределов продолжительности контейнера, например общего тома или узла подключенного тома.</span><span class="sxs-lookup"><span data-stu-id="99f43-208">A folder that's a Docker volume that persists beyond the container's lifetime, such as a shared volume or a host-mounted volume.</span></span>
* <span data-ttu-id="99f43-209">Внешнего поставщика, таких как [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) или [Redis](https://redis.io/).</span><span class="sxs-lookup"><span data-stu-id="99f43-209">An external provider, such as [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) or [Redis](https://redis.io/).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="99f43-210">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="99f43-210">Additional resources</span></span>

* <xref:security/data-protection/configuration/non-di-scenarios>
* <xref:security/data-protection/configuration/machine-wide-policy>
* <xref:host-and-deploy/web-farm>
