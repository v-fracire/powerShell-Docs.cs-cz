---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: PackageManagementSource prostředek DSC
ms.openlocfilehash: 3e67cec9058ecb0e43f882f98f5ec8b92e261a09
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="dsc-packagemanagementsource-resource"></a><span data-ttu-id="79c23-103">PackageManagementSource prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="79c23-103">DSC PackageManagementSource Resource</span></span>

> <span data-ttu-id="79c23-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="79c23-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="79c23-105">**PackageManagementSource** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro zaregistrovat nebo zrušit registraci zdroje správy balíčků na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="79c23-105">The **PackageManagementSource** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to register or unregister Package Management sources on a target node.</span></span> <span data-ttu-id="79c23-106">**Balíček správy zdroje registrované tímto způsobem je zaregistrovaný v kontextu systému, použít účet System nebo modul DSC.**</span><span class="sxs-lookup"><span data-stu-id="79c23-106">**Package Management sources registered in this way are registered under the System context, usable by the System account or by the DSC engine.**</span></span> <span data-ttu-id="79c23-107">Vyžaduje tento prostředek **PackageManagement** modulu, k dispozici z http://PowerShellGallery.com.</span><span class="sxs-lookup"><span data-stu-id="79c23-107">This resource requires the **PackageManagement** module, available from http://PowerShellGallery.com.</span></span>

## <a name="syntax"></a><span data-ttu-id="79c23-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="79c23-108">Syntax</span></span>

```
PSModule [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ InstallationPolicy = [string] ]
    [ ProviderName = [string] ]
    [ SourceUri = [string] ]
    [ SourceCredential = [PSCredential] ]
}
```

## <a name="properties"></a><span data-ttu-id="79c23-109">Properties</span><span class="sxs-lookup"><span data-stu-id="79c23-109">Properties</span></span>
|  <span data-ttu-id="79c23-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="79c23-110">Property</span></span>  |  <span data-ttu-id="79c23-111">Popis</span><span class="sxs-lookup"><span data-stu-id="79c23-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="79c23-112">Název</span><span class="sxs-lookup"><span data-stu-id="79c23-112">Name</span></span>| <span data-ttu-id="79c23-113">Určuje název zdroje balíčku, který má být zaregistrován nebo zrušit její registraci v systému.</span><span class="sxs-lookup"><span data-stu-id="79c23-113">Specifies the name of the package source to be registered or unregistered on your system.</span></span>|
| <span data-ttu-id="79c23-114">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="79c23-114">Ensure</span></span>| <span data-ttu-id="79c23-115">Určuje, zda zdroj balíčku má být zaregistrován nebo zrušit její registraci.</span><span class="sxs-lookup"><span data-stu-id="79c23-115">Determines whether the package source is to be registered or unregistered.</span></span>|
| <span data-ttu-id="79c23-116">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="79c23-116">InstallationPolicy</span></span>| <span data-ttu-id="79c23-117">Určuje, zda je zdroj balíčku důvěryhodný.</span><span class="sxs-lookup"><span data-stu-id="79c23-117">Determines whether you trust the package source.</span></span> <span data-ttu-id="79c23-118">Jeden z: "Nedůvěryhodná", "Důvěryhodné".</span><span class="sxs-lookup"><span data-stu-id="79c23-118">One of: "Untrusted", "Trusted".</span></span>|
| <span data-ttu-id="79c23-119">ProviderName</span><span class="sxs-lookup"><span data-stu-id="79c23-119">ProviderName</span></span>| <span data-ttu-id="79c23-120">Určuje název zprostředkovatele OneGet, pomocí kterého můžete Interoperabilita s zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="79c23-120">Specifies the name of the OneGet provider through which you can interop with the package source.</span></span>|
| <span data-ttu-id="79c23-121">SourceUri</span><span class="sxs-lookup"><span data-stu-id="79c23-121">SourceUri</span></span>| <span data-ttu-id="79c23-122">Určuje identifikátor URI zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="79c23-122">Specifies the URI of the package source.</span></span>|
| <span data-ttu-id="79c23-123">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="79c23-123">SourceCredential</span></span>| <span data-ttu-id="79c23-124">Poskytuje přístup k balíčku na vzdáleného zdroje.</span><span class="sxs-lookup"><span data-stu-id="79c23-124">Provides access to the package on a remote source.</span></span>|

## <a name="example"></a><span data-ttu-id="79c23-125">Příklad</span><span class="sxs-lookup"><span data-stu-id="79c23-125">Example</span></span>

<span data-ttu-id="79c23-126">Zaregistruje v tomto příkladu http://nuget.org zdroje balíčku pomocí **PackageManagementSource** prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="79c23-126">This example registers the http://nuget.org package source using the **PackageManagementSource** DSC resource.</span></span>

```powershell
Configuration PackageManagementSourceTest
{
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present"
        Name        = "MyNuget"
        ProviderName= "Nuget"
        SourceUri   = "http://nuget.org/api/v2/"
        InstallationPolicy ="Trusted"
    }
}
```