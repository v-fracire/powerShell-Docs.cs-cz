---
ms.date: 06/20/2018
keywords: DSC, powershell, konfigurace, instalační program
title: PackageManagementSource prostředků DSC
ms.openlocfilehash: e51b5318288bef458567dd4b58d17caaea3ed69b
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048113"
---
# <a name="dsc-packagemanagementsource-resource"></a><span data-ttu-id="2c44e-103">PackageManagementSource prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="2c44e-103">DSC PackageManagementSource Resource</span></span>

> <span data-ttu-id="2c44e-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0, prostředí Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="2c44e-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="2c44e-105">**PackageManagementSource** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro zaregistrovat nebo zrušit registraci balíčku správy zdrojů na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="2c44e-105">The **PackageManagementSource** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to register or unregister Package Management sources on a target node.</span></span> <span data-ttu-id="2c44e-106">**Balíček správy zdrojů zaregistrovaných tímto způsobem jsou registrovány v kontextu systému, použít systémový účet nebo modulem DSC.**</span><span class="sxs-lookup"><span data-stu-id="2c44e-106">**Package Management sources registered in this way are registered under the System context, usable by the System account or by the DSC engine.**</span></span> <span data-ttu-id="2c44e-107">Vyžaduje tento prostředek **PackageManagement** modulu, k dispozici z http://PowerShellGallery.com.</span><span class="sxs-lookup"><span data-stu-id="2c44e-107">This resource requires the **PackageManagement** module, available from http://PowerShellGallery.com.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c44e-108">**PackageManagement** modul by měl být dlouhý aspoň verzi 1.1.7.0 pro následující vlastnost informace správné.</span><span class="sxs-lookup"><span data-stu-id="2c44e-108">The **PackageManagement** module should be at least version 1.1.7.0 for the following property information to be correct.</span></span>

## <a name="syntax"></a><span data-ttu-id="2c44e-109">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="2c44e-109">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="2c44e-110">Properties</span><span class="sxs-lookup"><span data-stu-id="2c44e-110">Properties</span></span>

|  <span data-ttu-id="2c44e-111">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="2c44e-111">Property</span></span>  |  <span data-ttu-id="2c44e-112">Popis</span><span class="sxs-lookup"><span data-stu-id="2c44e-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="2c44e-113">Name</span><span class="sxs-lookup"><span data-stu-id="2c44e-113">Name</span></span>| <span data-ttu-id="2c44e-114">Určuje název balíčku zdroj, který má být registrováno nebo Odregistrováno ve vašem systému.</span><span class="sxs-lookup"><span data-stu-id="2c44e-114">Specifies the name of the package source to be registered or unregistered on your system.</span></span>|
| <span data-ttu-id="2c44e-115">ProviderName</span><span class="sxs-lookup"><span data-stu-id="2c44e-115">ProviderName</span></span>| <span data-ttu-id="2c44e-116">Určuje název zprostředkovatel oneget pro balíčky, pomocí kterého můžete zprostředkovatele komunikace s objekty zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="2c44e-116">Specifies the name of the OneGet provider through which you can interop with the package source.</span></span>|
| <span data-ttu-id="2c44e-117">SourceLocation</span><span class="sxs-lookup"><span data-stu-id="2c44e-117">SourceLocation</span></span>| <span data-ttu-id="2c44e-118">Určuje identifikátor URI zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="2c44e-118">Specifies the URI of the package source.</span></span>|
| <span data-ttu-id="2c44e-119">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="2c44e-119">Ensure</span></span>| <span data-ttu-id="2c44e-120">Určuje, zda zdroj balíčku registrováno nebo odregistrováno.</span><span class="sxs-lookup"><span data-stu-id="2c44e-120">Determines whether the package source is to be registered or unregistered.</span></span>|
| <span data-ttu-id="2c44e-121">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="2c44e-121">InstallationPolicy</span></span>| <span data-ttu-id="2c44e-122">Použít poskytovatelé jako je předdefinovaný poskytovatel Nuget.</span><span class="sxs-lookup"><span data-stu-id="2c44e-122">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="2c44e-123">Určuje, zda důvěřujete zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="2c44e-123">Determines whether you trust the package's source.</span></span> <span data-ttu-id="2c44e-124">Jedna z: "Nedůvěryhodné", "důvěryhodné".</span><span class="sxs-lookup"><span data-stu-id="2c44e-124">One of: "Untrusted", "Trusted".</span></span>|
| <span data-ttu-id="2c44e-125">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="2c44e-125">SourceCredential</span></span>| <span data-ttu-id="2c44e-126">Poskytuje přístup k balíčku na vzdáleného zdroje.</span><span class="sxs-lookup"><span data-stu-id="2c44e-126">Provides access to the package on a remote source.</span></span>|

## <a name="example"></a><span data-ttu-id="2c44e-127">Příklad</span><span class="sxs-lookup"><span data-stu-id="2c44e-127">Example</span></span>

<span data-ttu-id="2c44e-128">Registruje v tomto příkladu http://nuget.org pomocí zdroje balíčku **PackageManagementSource** prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="2c44e-128">This example registers the http://nuget.org package source using the **PackageManagementSource** DSC resource.</span></span>

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