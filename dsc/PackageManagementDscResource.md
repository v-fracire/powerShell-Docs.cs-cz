---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "PackageManagement prostředek DSC"
ms.openlocfilehash: 4cd7625af7ed0bb3fe971c826ac2075841cdfdc5
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-packagemanagement-resource"></a><span data-ttu-id="c70b0-103">PackageManagement prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="c70b0-103">DSC PackageManagement Resource</span></span>

> <span data-ttu-id="c70b0-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="c70b0-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="c70b0-105">**PackageManagement** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro instalaci nebo odinstalaci balíčků správy balíčků na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="c70b0-105">The **PackageManagement** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall Package Management packages on a target node.</span></span> <span data-ttu-id="c70b0-106">Vyžaduje tento prostředek **PackageManagement** modulu, k dispozici z http://PowerShellGallery.com.</span><span class="sxs-lookup"><span data-stu-id="c70b0-106">This resource requires the **PackageManagement** module, available from http://PowerShellGallery.com.</span></span>

## <a name="syntax"></a><span data-ttu-id="c70b0-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="c70b0-107">Syntax</span></span>

```
PackageManagement [string] #ResourceName
{
    Name = [string]
    [ Source = [string] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ RequiredVersion = [string] ]
    [ MinimumVersion = [string] ]
    [ MaximumVersion = [string] ]
    [ SourceCredential = [PSCredential] ]
    [ ProviderName = [string] ]
    [ AdditionalParameters = [Microsoft.Management.Infrastructure.CimInstance[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="c70b0-108">Properties</span><span class="sxs-lookup"><span data-stu-id="c70b0-108">Properties</span></span>
|  <span data-ttu-id="c70b0-109">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="c70b0-109">Property</span></span>  |  <span data-ttu-id="c70b0-110">Popis</span><span class="sxs-lookup"><span data-stu-id="c70b0-110">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="c70b0-111">Název</span><span class="sxs-lookup"><span data-stu-id="c70b0-111">Name</span></span>| <span data-ttu-id="c70b0-112">Určuje název balíčku, který má být nainstalována nebo odinstalována.</span><span class="sxs-lookup"><span data-stu-id="c70b0-112">Specifies the name of the Package to be installed or uninstalled.</span></span>| 
| <span data-ttu-id="c70b0-113">Zdroj</span><span class="sxs-lookup"><span data-stu-id="c70b0-113">Source</span></span>| <span data-ttu-id="c70b0-114">Určuje název zdroje balíčku, které lze nalézt balíček.</span><span class="sxs-lookup"><span data-stu-id="c70b0-114">Specifies the name of the package source where the package can be found.</span></span> <span data-ttu-id="c70b0-115">To může být identifikátor URI nebo zdroj zaregistrována Register-PackageSource nebo PackageManagementSource DSC prostředek.</span><span class="sxs-lookup"><span data-stu-id="c70b0-115">This can either be a URI or a source registered with Register-PackageSource or PackageManagementSource DSC resource.</span></span> <span data-ttu-id="c70b0-116">Prostředek DSC MSFT_PackageManagementSource taky moct registrovat zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="c70b0-116">The DSC resource MSFT_PackageManagementSource can also register a package source.</span></span>| 
| <span data-ttu-id="c70b0-117">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="c70b0-117">Ensure</span></span>| <span data-ttu-id="c70b0-118">Určuje, zda balíček má být nainstalována nebo odinstalována.</span><span class="sxs-lookup"><span data-stu-id="c70b0-118">Determines whether the package is to be installed or uninstalled.</span></span>| 
| <span data-ttu-id="c70b0-119">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="c70b0-119">RequiredVersion</span></span>| <span data-ttu-id="c70b0-120">Určuje přesnou verzi balíčku, který chcete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="c70b0-120">Specifies the exact version of the package that you want to install.</span></span> <span data-ttu-id="c70b0-121">Pokud tento parametr nezadáte, tento prostředek DSC nainstaluje na nejnovější dostupnou verzi balíčku, který splňuje všechny maximální verze zadaná v parametru MaximumVersion rovněž.</span><span class="sxs-lookup"><span data-stu-id="c70b0-121">If you do not specify this parameter, this DSC resource installs the newest available version of the package that also satisfies any maximum version specified by the MaximumVersion parameter.</span></span>| 
| <span data-ttu-id="c70b0-122">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="c70b0-122">MinimumVersion</span></span>| <span data-ttu-id="c70b0-123">Určuje minimální povolená verzi balíčku, který chcete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="c70b0-123">Specifies the minimum allowed version of the package that you want to install.</span></span> <span data-ttu-id="c70b0-124">Pokud tento parametr, tento intalls prostředků DSC nejvyšší dostupné verze balíčku, který splňuje všechny maximální zadaná verze zadané parametrem MaximumVersion rovněž nepřidávejte.</span><span class="sxs-lookup"><span data-stu-id="c70b0-124">If you do not add this parameter, this DSC resource intalls the highest available version of the package that also satisfies any maximum specified version specified by the MaximumVersion parameter.</span></span>| 
| <span data-ttu-id="c70b0-125">MaximumVersion</span><span class="sxs-lookup"><span data-stu-id="c70b0-125">MaximumVersion</span></span>| <span data-ttu-id="c70b0-126">Určuje maximální povolený verze balíčku, který chcete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="c70b0-126">Specifies the maximum allowed version of the package that you want to install.</span></span> <span data-ttu-id="c70b0-127">Pokud tento parametr nezadáte, tento prostředek DSC nainstaluje nejvyšší číslované dostupná verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="c70b0-127">If you do not specify this parameter, this DSC resource installs the highest-numbered available version of the package.</span></span>| 
| <span data-ttu-id="c70b0-128">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="c70b0-128">SourceCredential</span></span> | <span data-ttu-id="c70b0-129">Určuje uživatelský účet, který má práva pro instalaci balíčku pro zadaný balíček zprostředkovatele nebo zdroje.</span><span class="sxs-lookup"><span data-stu-id="c70b0-129">Specifies a user account that has rights to install a package for a specified package provider or source.</span></span>| 
| <span data-ttu-id="c70b0-130">ProviderName</span><span class="sxs-lookup"><span data-stu-id="c70b0-130">ProviderName</span></span>| <span data-ttu-id="c70b0-131">Určuje název zprostředkovatele balíček do které chcete obor vyhledávání balíčku.</span><span class="sxs-lookup"><span data-stu-id="c70b0-131">Specifies a package provider name to which to scope your package search.</span></span> <span data-ttu-id="c70b0-132">Název zprostředkovatele balíček můžete získat spuštěním rutiny Get-PackageProvider.</span><span class="sxs-lookup"><span data-stu-id="c70b0-132">You can get package provider names by running the Get-PackageProvider cmdlet.</span></span>| 
| <span data-ttu-id="c70b0-133">Další_parametry</span><span class="sxs-lookup"><span data-stu-id="c70b0-133">AdditionalParameters</span></span>| <span data-ttu-id="c70b0-134">Zprostředkovatel konkrétní parametry, které jsou předány jako zatřiďovací tabulky.</span><span class="sxs-lookup"><span data-stu-id="c70b0-134">Provider specific parameters that are passed as an Hashtable.</span></span> <span data-ttu-id="c70b0-135">Například pro zprostředkovatele NuGet můžete předat další parametry, jako je Cílová_cesta.</span><span class="sxs-lookup"><span data-stu-id="c70b0-135">For example, for NuGet provider you can pass additional parameters like DestinationPath.</span></span>| 

## <a name="additional-parameters"></a><span data-ttu-id="c70b0-136">Další parametry</span><span class="sxs-lookup"><span data-stu-id="c70b0-136">Additional Parameters</span></span>
<span data-ttu-id="c70b0-137">V následující tabulce je uveden seznam možností pro vlastnost Další_parametry.</span><span class="sxs-lookup"><span data-stu-id="c70b0-137">The following table lists options for the AdditionalParameters property.</span></span>
|  <span data-ttu-id="c70b0-138">Parametr</span><span class="sxs-lookup"><span data-stu-id="c70b0-138">Parameter</span></span>  | <span data-ttu-id="c70b0-139">Popis</span><span class="sxs-lookup"><span data-stu-id="c70b0-139">Description</span></span>   | 
|---|---|
| <span data-ttu-id="c70b0-140">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="c70b0-140">DestinationPath</span></span>| <span data-ttu-id="c70b0-141">Používá zprostředkovatele například předdefinované zprostředkovatele Nuget.</span><span class="sxs-lookup"><span data-stu-id="c70b0-141">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="c70b0-142">Určuje umístění souboru, kam chcete balíček, který má být nainstalován.</span><span class="sxs-lookup"><span data-stu-id="c70b0-142">Specifies a file location where you want the package to be installed.</span></span>|
| <span data-ttu-id="c70b0-143">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="c70b0-143">InstallationPolicy</span></span>| <span data-ttu-id="c70b0-144">Používá zprostředkovatele například předdefinované zprostředkovatele Nuget.</span><span class="sxs-lookup"><span data-stu-id="c70b0-144">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="c70b0-145">Určuje, zda je důvěryhodné zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="c70b0-145">Determines whether you trust the package's source.</span></span> <span data-ttu-id="c70b0-146">Jeden z: "Nedůvěryhodná", "Důvěryhodné".</span><span class="sxs-lookup"><span data-stu-id="c70b0-146">One of: "Untrusted", "Trusted".</span></span>|

## <a name="example"></a><span data-ttu-id="c70b0-147">Příklad</span><span class="sxs-lookup"><span data-stu-id="c70b0-147">Example</span></span>

<span data-ttu-id="c70b0-148">Tento příklad nainstaluje **JQuery** balíček NuGet a **GistProvider** pomocí modulu prostředí PowerShell **PackageManagement** prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="c70b0-148">This example installs the **JQuery** NuGet package and **GistProvider** PowerShell module using the **PackageManagement** DSC resource.</span></span> <span data-ttu-id="c70b0-149">Tento příklad nejprve zajišťuje zdroje požadovaný balíček jsou k dispozici, pak definuje očekávaný stav **JQuery** a **GistProvider** balíčky (NuGet a prostředí PowerShell, v uvedeném pořadí).</span><span class="sxs-lookup"><span data-stu-id="c70b0-149">This example first ensures the required package sources are available then defines the expected state of the **JQuery** and **GistProvider** packages (NuGet and PowerShell, respectively).</span></span>

```powershell
Configuration PackageTest
{    
    PackageManagementSource SourceRepository 
    { 
        Ensure      = "Present" 
        Name        = "MyNuget" 
        ProviderName= "Nuget" 
        SourceUri   = "http://nuget.org/api/v2/"   
        InstallationPolicy ="Trusted" 
    }    
    
    PackageManagementSource PSGallery 
    { 
        Ensure      = "Present" 
        Name        = "psgallery" 
        ProviderName= "PowerShellGet" 
        SourceUri   = "https://www.powershellgallery.com/api/v2/"   
        InstallationPolicy ="Trusted" 
    } 
          
    PackageManagement NugetPackage 
    { 
        Ensure               = "Present"  
        Name                 = "JQuery"
        AdditionalParameters = "$env:HomeDrive\nuget"
        RequiredVersion      = "2.0.1" 
        DependsOn            = "[PackageManagementSource]SourceRepository" 
    }
    
    PackageManagement PSModule 
    { 
        Ensure               = "Present"  
        Name                 = "gistprovider"
        Source               = "PSGallery"
        DependsOn            = "[PackageManagementSource]PSGallery" 
    }
}
```

