---
ms.date: 06/20/2018
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: PackageManagementSource prostředek DSC
ms.openlocfilehash: 5d049b05c387cafe27edb202d569852b10852dce
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2018
ms.locfileid: "34753766"
---
# <a name="dsc-packagemanagementsource-resource"></a><span data-ttu-id="ba4e6-103">PackageManagementSource prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="ba4e6-103">DSC PackageManagementSource Resource</span></span>

> <span data-ttu-id="ba4e6-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0, 5.1 prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba4e6-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="ba4e6-105">**PackageManagementSource** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro zaregistrovat nebo zrušit registraci zdroje správy balíčků na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="ba4e6-105">The **PackageManagementSource** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to register or unregister Package Management sources on a target node.</span></span> <span data-ttu-id="ba4e6-106">**Balíček správy zdroje registrované tímto způsobem je zaregistrovaný v kontextu systému, použít účet System nebo modul DSC.**</span><span class="sxs-lookup"><span data-stu-id="ba4e6-106">**Package Management sources registered in this way are registered under the System context, usable by the System account or by the DSC engine.**</span></span> <span data-ttu-id="ba4e6-107">Vyžaduje tento prostředek **PackageManagement** modulu, k dispozici z http://PowerShellGallery.com.</span><span class="sxs-lookup"><span data-stu-id="ba4e6-107">This resource requires the **PackageManagement** module, available from http://PowerShellGallery.com.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba4e6-108">**PackageManagement** modulu by měla být minimálně verze 1.1.7.0 následující vlastnost informace správné.</span><span class="sxs-lookup"><span data-stu-id="ba4e6-108">The **PackageManagement** module should be at least version 1.1.7.0 for the following property information to be correct.</span></span>

## <a name="syntax"></a><span data-ttu-id="ba4e6-109">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="ba4e6-109">Syntax</span></span>

```
PackageManagementSource [String] #ResourceName
{
    Name = [string]
    ProviderName = [string]
    SourceLocation = [string]
    [DependsOn = [string[]]]
    [Ensure = [string]{ Absent | Present }]
    [InstallationPolicy = [string]{ Trusted | Untrusted }]
    [PsDscRunAsCredential = [PSCredential]]
    [SourceCredential = [PSCredential]]
}
```

## <a name="properties"></a><span data-ttu-id="ba4e6-110">Properties</span><span class="sxs-lookup"><span data-stu-id="ba4e6-110">Properties</span></span>

|  <span data-ttu-id="ba4e6-111">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="ba4e6-111">Property</span></span>  |  <span data-ttu-id="ba4e6-112">Popis</span><span class="sxs-lookup"><span data-stu-id="ba4e6-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="ba4e6-113">Název</span><span class="sxs-lookup"><span data-stu-id="ba4e6-113">Name</span></span>| <span data-ttu-id="ba4e6-114">Určuje název zdroje balíčku, který má být zaregistrován nebo zrušit její registraci v systému.</span><span class="sxs-lookup"><span data-stu-id="ba4e6-114">Specifies the name of the package source to be registered or unregistered on your system.</span></span>|
| <span data-ttu-id="ba4e6-115">ProviderName</span><span class="sxs-lookup"><span data-stu-id="ba4e6-115">ProviderName</span></span>| <span data-ttu-id="ba4e6-116">Určuje název zprostředkovatele OneGet, pomocí kterého můžete Interoperabilita s zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="ba4e6-116">Specifies the name of the OneGet provider through which you can interop with the package source.</span></span>|
| <span data-ttu-id="ba4e6-117">SourceLocation</span><span class="sxs-lookup"><span data-stu-id="ba4e6-117">SourceLocation</span></span>| <span data-ttu-id="ba4e6-118">Určuje identifikátor URI zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="ba4e6-118">Specifies the URI of the package source.</span></span>|
| <span data-ttu-id="ba4e6-119">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="ba4e6-119">Ensure</span></span>| <span data-ttu-id="ba4e6-120">Určuje, zda zdroj balíčku má být zaregistrován nebo zrušit její registraci.</span><span class="sxs-lookup"><span data-stu-id="ba4e6-120">Determines whether the package source is to be registered or unregistered.</span></span>|
| <span data-ttu-id="ba4e6-121">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="ba4e6-121">InstallationPolicy</span></span>| <span data-ttu-id="ba4e6-122">Používá zprostředkovatele například předdefinované zprostředkovatele Nuget.</span><span class="sxs-lookup"><span data-stu-id="ba4e6-122">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="ba4e6-123">Určuje, zda je důvěryhodné zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="ba4e6-123">Determines whether you trust the package's source.</span></span> <span data-ttu-id="ba4e6-124">Jeden z: "Nedůvěryhodná", "Důvěryhodné".</span><span class="sxs-lookup"><span data-stu-id="ba4e6-124">One of: "Untrusted", "Trusted".</span></span>|
| <span data-ttu-id="ba4e6-125">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="ba4e6-125">SourceCredential</span></span>| <span data-ttu-id="ba4e6-126">Poskytuje přístup k balíčku na vzdáleného zdroje.</span><span class="sxs-lookup"><span data-stu-id="ba4e6-126">Provides access to the package on a remote source.</span></span>|

## <a name="example"></a><span data-ttu-id="ba4e6-127">Příklad</span><span class="sxs-lookup"><span data-stu-id="ba4e6-127">Example</span></span>

<span data-ttu-id="ba4e6-128">Zaregistruje v tomto příkladu http://nuget.org zdroje balíčku pomocí **PackageManagementSource** prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="ba4e6-128">This example registers the http://nuget.org package source using the **PackageManagementSource** DSC resource.</span></span>

```powershell
Configuration PackageManagementSourceTest
{
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present"
        Name        = "MyNuget"
        ProviderName= "Nuget"
        SourceLocation   = "http://nuget.org/api/v2/"
        InstallationPolicy ="Trusted"
    }
}
```