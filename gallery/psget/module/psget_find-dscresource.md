---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: "Najít DscResource"
ms.openlocfilehash: 37ba7925d6f73c453126f25e0818b3f8839d3b3b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="find-dscresource"></a><span data-ttu-id="ca964-103">Najít DscResource</span><span class="sxs-lookup"><span data-stu-id="ca964-103">Find-DscResource</span></span>

<span data-ttu-id="ca964-104">Vyhledá prostředky DSC v modulech.</span><span class="sxs-lookup"><span data-stu-id="ca964-104">Finds DSC Resources in modules.</span></span>

## <a name="description"></a><span data-ttu-id="ca964-105">Popis</span><span class="sxs-lookup"><span data-stu-id="ca964-105">Description</span></span>

<span data-ttu-id="ca964-106">Vyhledá rutinu najít DscResource [konfigurace požadovaného stavu (DSC)](https://msdn.microsoft.com/en-us/PowerShell/dsc/overview) prostředky obsažené v moduly, které odpovídají zadaným kritériím z registrovaných úložiště.</span><span class="sxs-lookup"><span data-stu-id="ca964-106">The Find-DscResource cmdlet finds [Desired State Configuration (DSC)](https://msdn.microsoft.com/en-us/PowerShell/dsc/overview) resources contained in modules that match the specified criteria from registered repositories.</span></span>
<span data-ttu-id="ca964-107">Pro každý modul, který tato rutina vyhledá najít DscResource vrátí objekt PSGetDscResourceInfo, který může vést k instalaci modulu pro instalaci modulů obsahující prostředky, které tato rutina vrací.</span><span class="sxs-lookup"><span data-stu-id="ca964-107">For each module that this cmdlet finds, Find-DscResource returns a PSGetDscResourceInfo object that you can pipe to Install-Module to install the modules containing the resources that this cmdlet returns.</span></span>

<span data-ttu-id="ca964-108">DSC je nová platforma pro správu v prostředí Windows PowerShell, který umožňuje nasazení a Správa konfigurační data pro softwaru služby a správu prostředí, ve kterém se tyto služby spuštěny.</span><span class="sxs-lookup"><span data-stu-id="ca964-108">DSC is a new management platform in Windows PowerShell that enables deploying and managing configuration data for software services and managing the environment in which these services run.</span></span>

<span data-ttu-id="ca964-109">Požadované prostředky konfigurace stavu (DSC) poskytují stavební bloky pro konfiguraci DSC.</span><span class="sxs-lookup"><span data-stu-id="ca964-109">Desired State Configuration (DSC) Resources provide the building blocks for a DSC configuration.</span></span> <span data-ttu-id="ca964-110">Prostředek zpřístupní vlastnosti, které může být nakonfigurované (schéma) a obsahuje funkce skriptu prostředí PowerShell, které místní Configuration Manager (LCM) žádostí na "jej tak".</span><span class="sxs-lookup"><span data-stu-id="ca964-110">A resource exposes properties that can be configured (schema) and contains the PowerShell script functions that the Local Configuration Manager (LCM) calls to "make it so".</span></span>

<span data-ttu-id="ca964-111">Prostředek může model něco jako obecný jako soubor nebo co nastavení serveru služby IIS.</span><span class="sxs-lookup"><span data-stu-id="ca964-111">A resource can model something as generic as a file or as specific as an IIS server setting.</span></span> <span data-ttu-id="ca964-112">Skupiny jako prostředky společně na modul DSC, který slouží k uspořádání všechny požadované soubory v strukturu, která je přenosný a zahrnuje metadata k identifikaci, jak jsou prostředky určena k použití.</span><span class="sxs-lookup"><span data-stu-id="ca964-112">Groups of like resources are combined in to a DSC Module, which organizes all the required files in to a structure that is portable and includes metadata to identify how the resources are intended to be used.</span></span>

- <span data-ttu-id="ca964-113">Najít DscResource můžete filtrovat s parametry verze: MinimumVersion, RequiredVersion, AllVersions.</span><span class="sxs-lookup"><span data-stu-id="ca964-113">Find-DscResource can filter with version parameters: MinimumVersion, RequiredVersion, AllVersions.</span></span>
  - <span data-ttu-id="ca964-114">Tyto parametry se vzájemně vylučují.</span><span class="sxs-lookup"><span data-stu-id="ca964-114">These parameters are mutually exclusive.</span></span>
  - <span data-ttu-id="ca964-115">Tyto parametry verze jsou povoleny pouze s názvem modulu single bez žádné zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="ca964-115">These version parameters are allowed only with the single module name without any wildcards.</span></span>
  - <span data-ttu-id="ca964-116">Pokud není zadán parametr RequiredVersion, vrátí DscResource najít nejnovější verzi modulu, která je rovna nebo větší než minimální verze zadaná nebo nejnovější verzi modulu, pokud je zadána žádná minimální verze.</span><span class="sxs-lookup"><span data-stu-id="ca964-116">If the RequiredVersion parameter is not specified, Find-DscResource returns the latest version of the module that is equal to or greater than the minimum version specified or the latest version of the module if no minimum version is specified.</span></span>
  - <span data-ttu-id="ca964-117">Pokud je zadán parametr RequiredVersion, najít DscResource pouze vrátí verzi modul, který přesně odpovídá zadaná verze.</span><span class="sxs-lookup"><span data-stu-id="ca964-117">If the RequiredVersion parameter is specified, Find-DscResource only returns the version of the module that exactly matches the specified version.</span></span>
- <span data-ttu-id="ca964-118">Najít DscResource můžete filtrovat podle metadata modulu s parametrem - značky</span><span class="sxs-lookup"><span data-stu-id="ca964-118">Find-DscResource can filter on module metadata with the -Tag parameter</span></span>
- <span data-ttu-id="ca964-119">Najít DscResource můžete filtrovat podle jazyka vyhledávání podle úložiště s parametrem - filtru.</span><span class="sxs-lookup"><span data-stu-id="ca964-119">Find-DscResource can filter on repository-specific search language with the -Filter parameter.</span></span>
- <span data-ttu-id="ca964-120">Najít DscResource můžete filtrovat podle moduly ze všech nebo několika registrované úložišť.</span><span class="sxs-lookup"><span data-stu-id="ca964-120">Find-DscResource can filter on modules from all or few of the registered repositories.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="ca964-121">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="ca964-121">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Find-DscResource -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="ca964-122">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="ca964-122">Cmdlet online help reference</span></span>

[<span data-ttu-id="ca964-123">Najít DscResource</span><span class="sxs-lookup"><span data-stu-id="ca964-123">Find-DscResource</span></span>](http://go.microsoft.com/fwlink/?LinkId=517196)

## <a name="example-commands"></a><span data-ttu-id="ca964-124">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="ca964-124">Example commands</span></span>
```powershell

# Find a specific DSC Resource
Find-DscResource -Name xIisFeatureDelegation

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
xIisFeatureDelegation               1.10.0.0   xWebAdministration                  PSGallery

# Find all available DSC Resources from all registered repositories
Find-DscResource

# Find a DSC resource by name
Find-DscResource -Name xWebsite

# Find multiple DSC Resources
Find-DscResource -Name xIisHandler, xFirewall

# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking
Find-DscResource -ModuleName xWebAdministration

# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

# Find available DSC Resources from few registered repositories
Find-DscResource -Repository PSGallery,PrivatePSGallery

# Find all DSC Resources in a specified repository
Find-DscResource -Repository PSGallery

# Find DSC Resources from all versions of a module
Find-DscResource -ModuleName xNetworking -AllVersions

# Find DSC Resources with module name and MinimumVersion.
Find-DscResource -ModuleName xNetworking -MinimumVersion 1.1

# Find DSC Resources with module name and exact version
Find-DscResource -ModuleName xNetworking -RequiredVersion 2.1.1

# Find DSC Resources defined modules with -Filter based search. -Filter searches in description and module names
Find-DscResource -Filter Domain

# Find all DSC Resources with tags Azure or DSC in module metadata
Find-DscResource -Tag Azure, DSC

```

