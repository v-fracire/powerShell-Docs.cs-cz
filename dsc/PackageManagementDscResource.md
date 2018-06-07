---
ms.date: 06/20/2018
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: PackageManagement prostředek DSC
ms.openlocfilehash: 3d52934b130d59acee4d7f8a92da2c743c1eb305
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2018
ms.locfileid: "34753783"
---
# <a name="dsc-packagemanagement-resource"></a><span data-ttu-id="1a871-103">PackageManagement prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="1a871-103">DSC PackageManagement Resource</span></span>

> <span data-ttu-id="1a871-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0, 5.1 prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a871-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="1a871-105">**PackageManagement** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro instalaci nebo odinstalaci balíčků správy balíčků na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="1a871-105">The **PackageManagement** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall Package Management packages on a target node.</span></span> <span data-ttu-id="1a871-106">Vyžaduje tento prostředek **PackageManagement** modulu, k dispozici z http://PowerShellGallery.com.</span><span class="sxs-lookup"><span data-stu-id="1a871-106">This resource requires the **PackageManagement** module, available from http://PowerShellGallery.com.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a871-107">**PackageManagement** modulu by měla být minimálně verze 1.1.7.0 následující vlastnost informace správné.</span><span class="sxs-lookup"><span data-stu-id="1a871-107">The **PackageManagement** module should be at least version 1.1.7.0 for the following property information to be correct.</span></span>

## <a name="syntax"></a><span data-ttu-id="1a871-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="1a871-108">Syntax</span></span>

```
PackageManagement [string] #ResourceName
{
    Name = [string]
    [AdditionalParameters = [HashTable]]
    [DependsOn = [string[]]]
    [Ensure = [string]{ Absent | Present }]
    [MaximumVersion = [string]]
    [MinimumVersion = [string]]
    [ProviderName = [string]]
    [PsDscRunAsCredential = [PSCredential]]
    [RequiredVersion = [string]]
    [Source = [string]]
    [SourceCredential = [PSCredential]]
}
```

## <a name="properties"></a><span data-ttu-id="1a871-109">Properties</span><span class="sxs-lookup"><span data-stu-id="1a871-109">Properties</span></span>

|  <span data-ttu-id="1a871-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="1a871-110">Property</span></span>  |  <span data-ttu-id="1a871-111">Popis</span><span class="sxs-lookup"><span data-stu-id="1a871-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="1a871-112">Název</span><span class="sxs-lookup"><span data-stu-id="1a871-112">Name</span></span>| <span data-ttu-id="1a871-113">Určuje název balíčku, který má být nainstalována nebo odinstalována.</span><span class="sxs-lookup"><span data-stu-id="1a871-113">Specifies the name of the Package to be installed or uninstalled.</span></span>|
| <span data-ttu-id="1a871-114">Další_parametry</span><span class="sxs-lookup"><span data-stu-id="1a871-114">AdditionalParameters</span></span>| <span data-ttu-id="1a871-115">Zprostředkovatel konkrétní zatřiďovací tabulku parametrů, které by byly předány `Get-Package -AdditionalArguments`.</span><span class="sxs-lookup"><span data-stu-id="1a871-115">Provider specific hashtable of parameters that would be passed to `Get-Package -AdditionalArguments`.</span></span> <span data-ttu-id="1a871-116">Například pro zprostředkovatele NuGet můžete předat další parametry, jako je Cílová_cesta.</span><span class="sxs-lookup"><span data-stu-id="1a871-116">For example, for NuGet provider you can pass additional parameters like DestinationPath.</span></span>|
| <span data-ttu-id="1a871-117">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="1a871-117">Ensure</span></span>| <span data-ttu-id="1a871-118">Určuje, zda balíček má být nainstalována nebo odinstalována.</span><span class="sxs-lookup"><span data-stu-id="1a871-118">Determines whether the package is to be installed or uninstalled.</span></span>|
| <span data-ttu-id="1a871-119">MaximumVersion</span><span class="sxs-lookup"><span data-stu-id="1a871-119">MaximumVersion</span></span>|<span data-ttu-id="1a871-120">Určuje maximální povolený verze balíčku, který chcete najít.</span><span class="sxs-lookup"><span data-stu-id="1a871-120">Specifies the maximum allowed version of the package that you want to find.</span></span> <span data-ttu-id="1a871-121">Pokud tento parametr nepřidáte, prostředek vyhledá nejvyšší dostupné verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="1a871-121">If you do not add this parameter, the resource finds the highest available version of the package.</span></span>|
| <span data-ttu-id="1a871-122">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="1a871-122">MinimumVersion</span></span>|<span data-ttu-id="1a871-123">Určuje minimální povolená verzi balíčku, který chcete najít.</span><span class="sxs-lookup"><span data-stu-id="1a871-123">Specifies the minimum allowed version of the package that you want to find.</span></span> <span data-ttu-id="1a871-124">Pokud tento parametr je nemůžete přidat, prostředek vyhledá nejvyšší dostupné verze balíčku, který také splňuje všechny maximální zadaná verze určeného _MaximumVersion_ parametr.</span><span class="sxs-lookup"><span data-stu-id="1a871-124">If you do not add this parameter, the resource finds the highest available version of the package that also satisfies any maximum specified version specified by the _MaximumVersion_ parameter.</span></span>|
| <span data-ttu-id="1a871-125">ProviderName</span><span class="sxs-lookup"><span data-stu-id="1a871-125">ProviderName</span></span>| <span data-ttu-id="1a871-126">Určuje název zprostředkovatele balíček do které chcete obor vyhledávání balíčku.</span><span class="sxs-lookup"><span data-stu-id="1a871-126">Specifies a package provider name to which to scope your package search.</span></span> <span data-ttu-id="1a871-127">Název zprostředkovatele balíček můžete získat spuštěním `Get-PackageProvider` rutiny.</span><span class="sxs-lookup"><span data-stu-id="1a871-127">You can get package provider names by running the `Get-PackageProvider` cmdlet.</span></span>|
| <span data-ttu-id="1a871-128">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="1a871-128">RequiredVersion</span></span>| <span data-ttu-id="1a871-129">Určuje přesnou verzi balíčku, který chcete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="1a871-129">Specifies the exact version of the package that you want to install.</span></span> <span data-ttu-id="1a871-130">Pokud tento parametr nezadáte, tento prostředek DSC nainstaluje na nejnovější dostupnou verzi balíčku, který také splňuje všechny maximální verze zadaná v _MaximumVersion_ parametr.</span><span class="sxs-lookup"><span data-stu-id="1a871-130">If you do not specify this parameter, this DSC resource installs the newest available version of the package that also satisfies any maximum version specified by the _MaximumVersion_ parameter.</span></span>|
| <span data-ttu-id="1a871-131">Zdroj</span><span class="sxs-lookup"><span data-stu-id="1a871-131">Source</span></span>| <span data-ttu-id="1a871-132">Určuje název zdroje balíčku, které lze nalézt balíček.</span><span class="sxs-lookup"><span data-stu-id="1a871-132">Specifies the name of the package source where the package can be found.</span></span> <span data-ttu-id="1a871-133">To může být identifikátor URI nebo zdroj zaregistrována `Register-PackageSource` nebo prostředek PackageManagementSource DSC.</span><span class="sxs-lookup"><span data-stu-id="1a871-133">This can either be a URI or a source registered with `Register-PackageSource` or PackageManagementSource DSC resource.</span></span>|
| <span data-ttu-id="1a871-134">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="1a871-134">SourceCredential</span></span> | <span data-ttu-id="1a871-135">Určuje uživatelský účet, který má práva pro instalaci balíčku pro zadaný balíček zprostředkovatele nebo zdroje.</span><span class="sxs-lookup"><span data-stu-id="1a871-135">Specifies a user account that has rights to install a package for a specified package provider or source.</span></span>|

## <a name="additional-parameters"></a><span data-ttu-id="1a871-136">Další parametry</span><span class="sxs-lookup"><span data-stu-id="1a871-136">Additional Parameters</span></span>

<span data-ttu-id="1a871-137">V následující tabulce je uveden seznam možností pro vlastnost Další_parametry.</span><span class="sxs-lookup"><span data-stu-id="1a871-137">The following table lists options for the AdditionalParameters property.</span></span>
|  <span data-ttu-id="1a871-138">Parametr</span><span class="sxs-lookup"><span data-stu-id="1a871-138">Parameter</span></span>  | <span data-ttu-id="1a871-139">Popis</span><span class="sxs-lookup"><span data-stu-id="1a871-139">Description</span></span>   |
|---|---|
| <span data-ttu-id="1a871-140">Cílová_cesta</span><span class="sxs-lookup"><span data-stu-id="1a871-140">DestinationPath</span></span>| <span data-ttu-id="1a871-141">Používá zprostředkovatele například předdefinované zprostředkovatele Nuget.</span><span class="sxs-lookup"><span data-stu-id="1a871-141">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="1a871-142">Určuje umístění souboru, kam chcete balíček, který má být nainstalován.</span><span class="sxs-lookup"><span data-stu-id="1a871-142">Specifies a file location where you want the package to be installed.</span></span>|
| <span data-ttu-id="1a871-143">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="1a871-143">InstallationPolicy</span></span>| <span data-ttu-id="1a871-144">Používá zprostředkovatele například předdefinované zprostředkovatele Nuget.</span><span class="sxs-lookup"><span data-stu-id="1a871-144">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="1a871-145">Určuje, zda je důvěryhodné zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="1a871-145">Determines whether you trust the package's source.</span></span> <span data-ttu-id="1a871-146">Jeden z: "Nedůvěryhodná", "Důvěryhodné".</span><span class="sxs-lookup"><span data-stu-id="1a871-146">One of: "Untrusted", "Trusted".</span></span>|

## <a name="example"></a><span data-ttu-id="1a871-147">Příklad</span><span class="sxs-lookup"><span data-stu-id="1a871-147">Example</span></span>

<span data-ttu-id="1a871-148">Tento příklad nainstaluje **JQuery** balíček NuGet a **GistProvider** pomocí modulu prostředí PowerShell **PackageManagement** prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="1a871-148">This example installs the **JQuery** NuGet package and **GistProvider** PowerShell module using the **PackageManagement** DSC resource.</span></span> <span data-ttu-id="1a871-149">Tento příklad nejprve zajišťuje zdroje požadovaný balíček jsou k dispozici, pak definuje očekávaný stav **JQuery** a **GistProvider** balíčky (NuGet a prostředí PowerShell, v uvedeném pořadí).</span><span class="sxs-lookup"><span data-stu-id="1a871-149">This example first ensures the required package sources are available then defines the expected state of the **JQuery** and **GistProvider** packages (NuGet and PowerShell, respectively).</span></span>

```powershell
Configuration PackageTest
{
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present"
        Name        = "MyNuget"
        ProviderName= "Nuget"
        SourceLocation   = "http://nuget.org/api/v2/"
        InstallationPolicy ="Trusted"
    }

    PackageManagementSource PSGallery
    {
        Ensure      = "Present"
        Name        = "psgallery"
        ProviderName= "PowerShellGet"
        SourceLocation   = "https://www.powershellgallery.com/api/v2/"
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