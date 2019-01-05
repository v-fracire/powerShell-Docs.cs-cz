---
ms.date: 06/20/2018
keywords: DSC, powershell, konfigurace, instalační program
title: PackageManagement prostředků DSC
ms.openlocfilehash: 18cbbfe0715c82dcfdf4a5fb6ee36ee814e43d3b
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048159"
---
# <a name="dsc-packagemanagement-resource"></a><span data-ttu-id="86863-103">PackageManagement prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="86863-103">DSC PackageManagement Resource</span></span>

<span data-ttu-id="86863-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0, prostředí Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="86863-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="86863-105">**PackageManagement** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro instalaci nebo odinstalaci balíčku správy balíčků na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="86863-105">The **PackageManagement** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall Package Management packages on a target node.</span></span> <span data-ttu-id="86863-106">Vyžaduje tento prostředek **PackageManagement** modulu, k dispozici z [ http://PowerShellGallery.com ](http://PowerShellGallery.com).</span><span class="sxs-lookup"><span data-stu-id="86863-106">This resource requires the **PackageManagement** module, available from [http://PowerShellGallery.com](http://PowerShellGallery.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86863-107">**PackageManagement** modul by měl být dlouhý aspoň verzi 1.1.7.0 pro následující vlastnost informace správné.</span><span class="sxs-lookup"><span data-stu-id="86863-107">The **PackageManagement** module should be at least version 1.1.7.0 for the following property information to be correct.</span></span>

## <a name="syntax"></a><span data-ttu-id="86863-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="86863-108">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="86863-109">Properties</span><span class="sxs-lookup"><span data-stu-id="86863-109">Properties</span></span>

| <span data-ttu-id="86863-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="86863-110">Property</span></span> | <span data-ttu-id="86863-111">Popis</span><span class="sxs-lookup"><span data-stu-id="86863-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="86863-112">Name</span><span class="sxs-lookup"><span data-stu-id="86863-112">Name</span></span>| <span data-ttu-id="86863-113">Určuje název balíčku, který má být nainstalována nebo odinstalována.</span><span class="sxs-lookup"><span data-stu-id="86863-113">Specifies the name of the Package to be installed or uninstalled.</span></span>|
| <span data-ttu-id="86863-114">Další_parametry</span><span class="sxs-lookup"><span data-stu-id="86863-114">AdditionalParameters</span></span>| <span data-ttu-id="86863-115">Zprostředkovatel konkrétní zatřiďovací tabulku parametrů, které by byly předány `Get-Package -AdditionalArguments`.</span><span class="sxs-lookup"><span data-stu-id="86863-115">Provider specific hashtable of parameters that would be passed to `Get-Package -AdditionalArguments`.</span></span> <span data-ttu-id="86863-116">Například pro zprostředkovatele NuGet můžete předat další parametry, jako je DestinationPath.</span><span class="sxs-lookup"><span data-stu-id="86863-116">For example, for NuGet provider you can pass additional parameters like DestinationPath.</span></span>|
| <span data-ttu-id="86863-117">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="86863-117">Ensure</span></span>| <span data-ttu-id="86863-118">Určuje, zda balíček nainstalovat nebo odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="86863-118">Determines whether the package is to be installed or uninstalled.</span></span>|
| <span data-ttu-id="86863-119">MaximumVersion</span><span class="sxs-lookup"><span data-stu-id="86863-119">MaximumVersion</span></span>|<span data-ttu-id="86863-120">Určuje maximální povolenou verzi balíčku, který má být nalezena.</span><span class="sxs-lookup"><span data-stu-id="86863-120">Specifies the maximum allowed version of the package that you want to find.</span></span> <span data-ttu-id="86863-121">Pokud nemůžete přidat tento parametr, vyhledá prostředek nejvyšší dostupnou verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="86863-121">If you do not add this parameter, the resource finds the highest available version of the package.</span></span>|
| <span data-ttu-id="86863-122">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="86863-122">MinimumVersion</span></span>|<span data-ttu-id="86863-123">Určuje minimální povolenou verzi balíčku, který má být nalezena.</span><span class="sxs-lookup"><span data-stu-id="86863-123">Specifies the minimum allowed version of the package that you want to find.</span></span> <span data-ttu-id="86863-124">Pokud nemůžete přidat tento parametr, prostředek vyhledá nejvyšší dostupnou verzi balíčku, který také splňuje všechny maximální zadaná verze určená _MaximumVersion_ parametru.</span><span class="sxs-lookup"><span data-stu-id="86863-124">If you do not add this parameter, the resource finds the highest available version of the package that also satisfies any maximum specified version specified by the _MaximumVersion_ parameter.</span></span>|
| <span data-ttu-id="86863-125">ProviderName</span><span class="sxs-lookup"><span data-stu-id="86863-125">ProviderName</span></span>| <span data-ttu-id="86863-126">Určuje název zprostředkovatele balíček do kterého chcete omezit rozsah hledání balíčku.</span><span class="sxs-lookup"><span data-stu-id="86863-126">Specifies a package provider name to which to scope your package search.</span></span> <span data-ttu-id="86863-127">Názvy balíčků zprostředkovatele můžete získat spuštěním `Get-PackageProvider` rutiny.</span><span class="sxs-lookup"><span data-stu-id="86863-127">You can get package provider names by running the `Get-PackageProvider` cmdlet.</span></span>|
| <span data-ttu-id="86863-128">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="86863-128">RequiredVersion</span></span>| <span data-ttu-id="86863-129">Určuje přesnou verzi balíčku, který chcete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="86863-129">Specifies the exact version of the package that you want to install.</span></span> <span data-ttu-id="86863-130">Pokud tento parametr nezadáte, tento prostředek DSC nainstaluje na nejnovější dostupnou verzi balíčku, který také splňuje všechny maximální verze určená _MaximumVersion_ parametru.</span><span class="sxs-lookup"><span data-stu-id="86863-130">If you do not specify this parameter, this DSC resource installs the newest available version of the package that also satisfies any maximum version specified by the _MaximumVersion_ parameter.</span></span>|
| <span data-ttu-id="86863-131">Zdroj</span><span class="sxs-lookup"><span data-stu-id="86863-131">Source</span></span>| <span data-ttu-id="86863-132">Určuje název zdroje balíčku, kde můžete najít balíček.</span><span class="sxs-lookup"><span data-stu-id="86863-132">Specifies the name of the package source where the package can be found.</span></span> <span data-ttu-id="86863-133">Může to být buď identifikátor URI nebo zdroj zaregistrovaného `Register-PackageSource` nebo prostředek DSC PackageManagementSource.</span><span class="sxs-lookup"><span data-stu-id="86863-133">This can either be a URI or a source registered with `Register-PackageSource` or PackageManagementSource DSC resource.</span></span>|
| <span data-ttu-id="86863-134">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="86863-134">SourceCredential</span></span> | <span data-ttu-id="86863-135">Určuje uživatelský účet, který má oprávnění k instalaci balíčku pro zadaný balíček poskytovatele nebo zdroj.</span><span class="sxs-lookup"><span data-stu-id="86863-135">Specifies a user account that has rights to install a package for a specified package provider or source.</span></span>|

## <a name="additional-parameters"></a><span data-ttu-id="86863-136">Další parametry</span><span class="sxs-lookup"><span data-stu-id="86863-136">Additional Parameters</span></span>

<span data-ttu-id="86863-137">V následující tabulce jsou uvedeny možnosti pro vlastnost Další_parametry.</span><span class="sxs-lookup"><span data-stu-id="86863-137">The following table lists options for the AdditionalParameters property.</span></span>

| <span data-ttu-id="86863-138">Parametr</span><span class="sxs-lookup"><span data-stu-id="86863-138">Parameter</span></span> | <span data-ttu-id="86863-139">Popis</span><span class="sxs-lookup"><span data-stu-id="86863-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="86863-140">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="86863-140">DestinationPath</span></span>| <span data-ttu-id="86863-141">Použít poskytovatelé jako je předdefinovaný poskytovatel Nuget.</span><span class="sxs-lookup"><span data-stu-id="86863-141">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="86863-142">Určuje umístění souboru, kam chcete balíček nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="86863-142">Specifies a file location where you want the package to be installed.</span></span>|
| <span data-ttu-id="86863-143">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="86863-143">InstallationPolicy</span></span>| <span data-ttu-id="86863-144">Použít poskytovatelé jako je předdefinovaný poskytovatel Nuget.</span><span class="sxs-lookup"><span data-stu-id="86863-144">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="86863-145">Určuje, zda důvěřujete zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="86863-145">Determines whether you trust the package's source.</span></span> <span data-ttu-id="86863-146">Jeden z: `Untrusted`, `Trusted`.</span><span class="sxs-lookup"><span data-stu-id="86863-146">One of: `Untrusted`, `Trusted`.</span></span>|

## <a name="example"></a><span data-ttu-id="86863-147">Příklad</span><span class="sxs-lookup"><span data-stu-id="86863-147">Example</span></span>

<span data-ttu-id="86863-148">Tento příklad nainstaluje **JQuery** balíčku NuGet a **GistProvider** pomocí modulu PowerShell **PackageManagement** prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="86863-148">This example installs the **JQuery** NuGet package and **GistProvider** PowerShell module using the **PackageManagement** DSC resource.</span></span> <span data-ttu-id="86863-149">V tomto příkladu nejdřív zajišťuje zdroje požadovaný balíček jsou k dispozici, pak určuje očekávaný stav **JQuery** a **GistProvider** balíčky (NuGet a prostředí PowerShell, v uvedeném pořadí).</span><span class="sxs-lookup"><span data-stu-id="86863-149">This example first ensures the required package sources are available then defines the expected state of the **JQuery** and **GistProvider** packages (NuGet and PowerShell, respectively).</span></span>

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