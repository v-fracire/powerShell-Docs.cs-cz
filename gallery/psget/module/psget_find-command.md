---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: "Najít – příkaz"
ms.openlocfilehash: f867f12b1c6efad30a04581c6f36c5a77a2fb2ae
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="find-command"></a><span data-ttu-id="86579-103">Najít – příkaz</span><span class="sxs-lookup"><span data-stu-id="86579-103">Find-Command</span></span>

<span data-ttu-id="86579-104">Vyhledá příkazy prostředí PowerShell v modulech.</span><span class="sxs-lookup"><span data-stu-id="86579-104">Finds PowerShell commands in modules.</span></span>

## <a name="description"></a><span data-ttu-id="86579-105">Popis</span><span class="sxs-lookup"><span data-stu-id="86579-105">Description</span></span>
<span data-ttu-id="86579-106">Najít – příkaz rutina vyhledá příkazy prostředí PowerShell jako rutiny, aliasy, funkce a pracovní postupy.</span><span class="sxs-lookup"><span data-stu-id="86579-106">The Find-Command cmdlet finds PowerShell commands such as cmdlets, aliases, functions, and workflows.</span></span> <span data-ttu-id="86579-107">Najít – příkaz vyhledá moduly v registrovaných úložiště.</span><span class="sxs-lookup"><span data-stu-id="86579-107">Find-Command searches modules in registered repositories.</span></span>
<span data-ttu-id="86579-108">U každého příkazu, který tato rutina vyhledá vrátí objekt PSGetCommandInfo.</span><span class="sxs-lookup"><span data-stu-id="86579-108">For each command that this cmdlet finds, it returns a PSGetCommandInfo object.</span></span> <span data-ttu-id="86579-109">Objekt PSGetCommandInfo můžete předat do rutiny Install-Module nainstalovat modul, který obsahuje příkaz.</span><span class="sxs-lookup"><span data-stu-id="86579-109">You can pass a PSGetCommandInfo object to the Install-Module cmdlet to install the module that contains the command.</span></span>

- <span data-ttu-id="86579-110">Najít – příkaz můžete filtrovat s parametry verze: MinimumVersion, RequiredVersion, AllVersions.</span><span class="sxs-lookup"><span data-stu-id="86579-110">Find-Command can filter with version parameters: MinimumVersion, RequiredVersion, AllVersions.</span></span>
  - <span data-ttu-id="86579-111">Tyto parametry se vzájemně vylučují.</span><span class="sxs-lookup"><span data-stu-id="86579-111">These parameters are mutually exclusive.</span></span>
  - <span data-ttu-id="86579-112">Tyto parametry verze jsou povoleny pouze s názvem modulu single bez žádné zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="86579-112">These version parameters are allowed only with the single module name without any wildcards.</span></span>
  - <span data-ttu-id="86579-113">Pokud není zadán parametr RequiredVersion, vrátí příkaz najít nejnovější verzi modulu, která je rovna nebo větší než minimální verze zadaná nebo nejnovější verzi modulu, pokud je zadána žádná minimální verze.</span><span class="sxs-lookup"><span data-stu-id="86579-113">If the RequiredVersion parameter is not specified, Find-Command returns the latest version of the module that is equal to or greater than the minimum version specified or the latest version of the module if no minimum version is specified.</span></span>
  - <span data-ttu-id="86579-114">Pokud je zadán parametr RequiredVersion, najít – příkaz vrátí jenom verzi modul, který přesně odpovídá zadaná verze.</span><span class="sxs-lookup"><span data-stu-id="86579-114">If the RequiredVersion parameter is specified, Find-Command only returns the version of the module that exactly matches the specified version.</span></span>
- <span data-ttu-id="86579-115">Najít – příkaz můžete filtrovat podle metadata modulu s parametrem - značky</span><span class="sxs-lookup"><span data-stu-id="86579-115">Find-Command can filter on module metadata with the -Tag parameter</span></span>
- <span data-ttu-id="86579-116">Najít – příkaz můžete filtrovat podle jazyka vyhledávání podle úložiště s parametrem - filtru.</span><span class="sxs-lookup"><span data-stu-id="86579-116">Find-Command can filter on repository-specific search language with the -Filter parameter.</span></span>
- <span data-ttu-id="86579-117">Najít – příkaz můžete filtrovat podle moduly ze všech nebo několika registrované úložišť.</span><span class="sxs-lookup"><span data-stu-id="86579-117">Find-Command can filter on modules from all or few of the registered repositories.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="86579-118">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="86579-118">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Find-Command -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="86579-119">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="86579-119">Cmdlet online help reference</span></span>

[<span data-ttu-id="86579-120">Najít – příkaz</span><span class="sxs-lookup"><span data-stu-id="86579-120">Find-Command</span></span>](http://go.microsoft.com/fwlink/?LinkId=733636)

## <a name="example-commands"></a><span data-ttu-id="86579-121">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="86579-121">Example commands</span></span>
```powershell

# Find a specific command
Find-Command -Name Get-ScriptAnalyzerRule

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Get-ScriptAnalyzerRule              1.5.0      PSScriptAnalyzer                    PSGallery

# Find multiple commands
Find-Command -Name Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

# Find all available commands from all registered repositories
Find-Command

# Find available commands from few registered repositories
Find-Command -Repository PSGallery,PrivatePSGallery

# Find all commands in a specified repository
Find-Command -Repository PSGallery

# Find a command defined in a specific module
Find-Command -Name Get-ScriptAnalyzerRule -Module PSScriptAnalyzer

# Find commands from all versions of a module
Find-Command -ModuleName PSReadline -AllVersions

# Find commands with module name and MinimumVersion.
Find-Command -ModuleName PSReadline -MinimumVersion 1.1

# Find commands with module name and exact version
Find-Command -ModuleName AzureRM -RequiredVersion 1.4.0

# Find commands defined modules with -Filter based search. -Filter searches in description and module names
Find-Command -Filter Cookbook
Find-Command -Filter RBAC

# Find all commands with tags Azure or DSC in module metadata
Find-Command -Tag Azure, DSC

```

