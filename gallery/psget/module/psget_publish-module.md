---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: Publikování modulu
ms.openlocfilehash: 8b73be2814678ce143cc5b53e2b8103b3297eb6a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="publish-module"></a><span data-ttu-id="b96e1-103">Publikování modulu</span><span class="sxs-lookup"><span data-stu-id="b96e1-103">Publish-Module</span></span>

<span data-ttu-id="b96e1-104">Publikuje zadaný modul z místního počítače do online galerie.</span><span class="sxs-lookup"><span data-stu-id="b96e1-104">Publishes a specified module from the local computer to an online gallery.</span></span>

## <a name="description"></a><span data-ttu-id="b96e1-105">Popis</span><span class="sxs-lookup"><span data-stu-id="b96e1-105">Description</span></span>

<span data-ttu-id="b96e1-106">**Publikovat modulu** rutiny publikuje modul do online galerie NuGet základě pomocí klíče rozhraní API, uložené v rámci profilu uživatele v galerii.</span><span class="sxs-lookup"><span data-stu-id="b96e1-106">The **Publish-Module** cmdlet publishes a module to an online NuGet-based gallery by using an API key, stored as part of a user's profile in the gallery.</span></span> <span data-ttu-id="b96e1-107">Zadaný modul pro publikování podle názvu modulu nebo cestě ke složce obsahující modul.</span><span class="sxs-lookup"><span data-stu-id="b96e1-107">You can specify the module to publish either by the module's name, or by the path to the folder containing the module.</span></span>

<span data-ttu-id="b96e1-108">Když zadáte modul podle názvu, **publikovat modulu** publikuje první modul, který bude nalezen spuštěním `Get-Module -ListAvailable <Name>`.</span><span class="sxs-lookup"><span data-stu-id="b96e1-108">When you specify a module by name, **Publish-Module** publishes the first module that would be found by running `Get-Module -ListAvailable <Name>`.</span></span> <span data-ttu-id="b96e1-109">Pokud zadáte minimální verze modulu k publikování, **publikovat modulu** publikuje první modul s verzí, která je větší než nebo rovna minimální verzi, která jste zadali.</span><span class="sxs-lookup"><span data-stu-id="b96e1-109">If you specify a minimum version of a module to publish, **Publish-Module** publishes the first module with a version that is greater than or equal to the minimum version that you have specified.</span></span>

<span data-ttu-id="b96e1-110">Publikování modul vyžaduje metadata, která se zobrazí na stránce Galerie pro modul.</span><span class="sxs-lookup"><span data-stu-id="b96e1-110">Publishing a module requires metadata that is displayed on the gallery page for the module.</span></span> <span data-ttu-id="b96e1-111">Požadovaná metadata zahrnuje modul název, verzi, popis a autora.</span><span class="sxs-lookup"><span data-stu-id="b96e1-111">Required metadata includes the module name, version, description, and author.</span></span> <span data-ttu-id="b96e1-112">I když většina metadata jsou převzaty z manifestu modulu, některá metadata musí být zadány v **publikovat modulu** parametry, například *značky, ReleaseNote, IconUri, ProjectUri,* a  *LicenseUri*, protože tyto parametry odpovídaly pole v galerii na základě NuGet.</span><span class="sxs-lookup"><span data-stu-id="b96e1-112">Although most metadata is taken from the module manifest, some metadata must be specified in **Publish-Module** parameters, such as *Tag, ReleaseNote, IconUri, ProjectUri,* and *LicenseUri*, because these parameters match fields in a NuGet-based gallery.</span></span>

<span data-ttu-id="b96e1-113">Parametr RequiredVersion vám umožní určit přesnou verzi modulu k publikování.</span><span class="sxs-lookup"><span data-stu-id="b96e1-113">The RequiredVersion parameter allows you to specify the exact version of a module to be published.</span></span>
<span data-ttu-id="b96e1-114">Parametr Path také podporuje základní cesta modulu se složkou verze.</span><span class="sxs-lookup"><span data-stu-id="b96e1-114">The Path parameter also supports the module base path with the version folder.</span></span>
<span data-ttu-id="b96e1-115">Parametr Force přepínač na rutinu modulu publikovat bootstraps NuGet.exe bez zobrazení výzvy.</span><span class="sxs-lookup"><span data-stu-id="b96e1-115">The Force switch parameter on Publish-Module cmdlet bootstraps the NuGet.exe without prompting.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="b96e1-116">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="b96e1-116">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Publish-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="b96e1-117">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="b96e1-117">Cmdlet online help reference</span></span>

[<span data-ttu-id="b96e1-118">Publish-Module</span><span class="sxs-lookup"><span data-stu-id="b96e1-118">Publish-Module</span></span>](http://go.microsoft.com/fwlink/?LinkID=398575)

## <a name="example-commands"></a><span data-ttu-id="b96e1-119">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="b96e1-119">Example commands</span></span>

```powershell
ContosoServer module with different versions to be published.
PS C:\\windows\\system32> Get-Module -Name ContosoServer -ListAvailable
Directory: C:\\Program Files\\WindowsPowerShell\\Modules
ModuleType Version Name ExportedCommands
---------- ------- ---- ----------------
Manifest 2.8 ContosoServer Get-ContosoServer
Manifest 2.0 ContosoServer Get-ContosoServer
Manifest 1.5 ContosoServer Get-ContosoServer
Manifest 1.0 ContosoServer Get-ContosoServer
PS C:\\windows\\system32> Publish-Module -Name ContosoServer -RequiredVersion 1.0 -Repository LocalRepo -NuGetApiKey Local-Repo-NuGet-ApiKey
PS C:\\windows\\system32> Find-Module -Name ContosoServer -Repository LocalRepo
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer LocalRepo ContosoServer module
PS C:\\windows\\system32> Publish-Module -Name ContosoServer -RequiredVersion 1.5 -Repository LocalRepo -NuGetApiKey Local-Repo-NuGet-ApiKey
PS C:\\windows\\system32> Find-Module -Name ContosoServer -Repository LocalRepo
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer LocalRepo ContosoServer module
1.5 ContosoServer LocalRepo ContosoServer module
PS C:\\windows\\system32> Publish-Module -Path "C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\2.0" -Repository LocalRepo -NuGetApiKey Local-Repo-NuGet-ApiKey
PS C:\\windows\\system32> Find-Module -Name ContosoServer -Repository LocalRepo
Version Name Repository Description
_------ ---- ---------- -----------
1.0 ContosoServer LocalRepo ContosoServer module
1.5 ContosoServer LocalRepo ContosoServer module
2.0 ContosoServer LocalRepo ContosoServer module
```

## <a name="publishing-a-module-with-dependencies"></a><span data-ttu-id="b96e1-120">Publikování modul s závislosti</span><span class="sxs-lookup"><span data-stu-id="b96e1-120">Publishing a module with dependencies</span></span>

### <a name="create-a-module-with-dependencies-and-version-range-specified-in-requiredmodules-property-of-its-module-manifest"></a><span data-ttu-id="b96e1-121">Vytvoření modulu s závislosti a rozsahu verze zadaná ve vlastnosti RequiredModules jeho manifestu modulu.</span><span class="sxs-lookup"><span data-stu-id="b96e1-121">Create a module with dependencies and version range specified in RequiredModules property of its module manifest.</span></span>

<span data-ttu-id="b96e1-122">**Poznámka:**</span><span class="sxs-lookup"><span data-stu-id="b96e1-122">**Note:**</span></span>
  - <span data-ttu-id="b96e1-123">\* je podporováno pouze v MaximumVersion a také musí být na konci řetězec verze.</span><span class="sxs-lookup"><span data-stu-id="b96e1-123">\* is supported only in MaximumVersion and also it should be at the end of version string.</span></span>
  - <span data-ttu-id="b96e1-124">\* se nahradí 999999999 v objektu verze.</span><span class="sxs-lookup"><span data-stu-id="b96e1-124">\* is replaced with 999999999 in the version object.</span></span>

```powershell
PS C:\windows\system32> $requiredModules = @( @{ModuleName = 'RequiredModule1'; ModuleVersion = '0.1'; MaximumVersion = '1.9'; }, @{ModuleName = 'RequiredModule2'; MaximumVersion = '1.*'; })

PS C:\windows\system32> cd C:\MyModules\ModuleWithDependencies

PS C:\MyModules\ModuleWithDependencies> New-ModuleManifest -Path .\ModuleWithDependencies.psd1 -ModuleVersion 1.0 -RequiredModules $requiredModules -Description 'ModuleWithDependencies demo module'
```

### <a name="publish-modulewithdependencies-module-with-dependencies-to-the-repository"></a><span data-ttu-id="b96e1-125">Modul ModuleWithDependencies s závislosti publikujte do úložiště.</span><span class="sxs-lookup"><span data-stu-id="b96e1-125">Publish ModuleWithDependencies module with dependencies to the repository.</span></span>

```powershell
PS C:\MyModules\ModuleWithDependencies> Publish-Module -Path C:\MyModules\ModuleWithDependencies -Repository LocalRepo
```

### <a name="find-modulewithdependencies-module-with-its-dependencies-by-specifying--includedependencies"></a><span data-ttu-id="b96e1-126">Vyhledání modulu ModuleWithDependencies s jeho závislé součásti zadáním - IncludeDependencies</span><span class="sxs-lookup"><span data-stu-id="b96e1-126">Find ModuleWithDependencies module with its dependencies by specifying -IncludeDependencies</span></span>

```powershell
PS C:\MyModules\ModuleWithDependencies> Find-Module -Name ModuleWithDependencies -Repository LocalRepo -IncludeDependencies

Version    Name                                Type       Repository           Description
-------    ----                                ----       ----------           -----------
1.0        ModuleWithDependencies              Module     localrepo            ModuleWithDependencies demo module
1.5        RequiredModule1                     Module     localrepo            RequiredModule1 module
1.5        RequiredModule2                     Module     localrepo            RequiredModule2 module
```

### <a name="install-the-modulewithdependencies-module-with-dependencies"></a><span data-ttu-id="b96e1-127">Nainstalujte modul ModuleWithDependencies se závislostmi.</span><span class="sxs-lookup"><span data-stu-id="b96e1-127">Install the ModuleWithDependencies module with dependencies.</span></span>
<span data-ttu-id="b96e1-128">Všimněte si, že verze rozsahy jsou dodržení během instalace závislostí.</span><span class="sxs-lookup"><span data-stu-id="b96e1-128">Note that version ranges are honored during the dependency installation.</span></span>

```powershell
PS C:\windows\system32> Get-InstalledModule
PS C:\windows\system32>
PS C:\windows\system32> Install-Module -Name ModuleWithDependencies -Repository LocalRepo
PS C:\windows\system32>
PS C:\windows\system32> Get-InstalledModule

Version    Name                                Type       Repository           Description
-------    ----                                ----       ----------           -----------
1.0        ModuleWithDependencies              Module     localrepo            ModuleWithDependencies demo module
1.5        RequiredModule1                     Module     localrepo            RequiredModule1 module
1.5        RequiredModule2                     Module     localrepo            RequiredModule2 module
```

### <a name="contents-of-modulewithdependencies2-module-manifest-file"></a><span data-ttu-id="b96e1-129">Soubor manifestu obsah ModuleWithDependencies2 modulu</span><span class="sxs-lookup"><span data-stu-id="b96e1-129">Contents of ModuleWithDependencies2 module manifest file</span></span>

```powershell
@{
# Version number of this module.
ModuleVersion = '2.0'
# ID used to uniquely identify this module
GUID = '0eae34da-99dd-4608-8d28-c614fe7b0841'
# Author of this module
Author = 'manikb'
# Company or vendor of this module
CompanyName = 'Unknown'
# Copyright statement for this module
Copyright = '(c) 2015 manikb. All rights reserved.'
# Description of the functionality provided by this module
Description = 'ModuleWithDependencies2 module'
# Modules that must be imported into the global environment prior to importing this module
RequiredModules = @('RequiredModule1',
@{ModuleName = 'RequiredModule2'; ModuleVersion = '2.0'; },
@{ModuleName = 'RequiredModule3'; RequiredVersion = '2.5'; },
@{ModuleName = 'RequiredModule4'; ModuleVersion = '1.1'; MaximumVersion = '2.0'; },
@{ModuleName = 'RequiredModule5'; MaximumVersion = '1.5'; })
# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
NestedModules = @('NestedRequiredModule1',
@{ModuleName = 'NestedRequiredModule2'; ModuleVersion = '2.0'; },
@{ModuleName = 'NestedRequiredModule3'; RequiredVersion = '2.5'; },
@{ModuleName = 'NestedRequiredModule4'; ModuleVersion = '0.7'; MaximumVersion = '2.4'; },
@{ModuleName = 'NestedRequiredModule5'; MaximumVersion = '1.6'; },'ModuleWithDependencies2.psm1')
# Functions to export from this module
FunctionsToExport = '\*'
# Cmdlets to export from this module
CmdletsToExport = '\*'
# Variables to export from this module
VariablesToExport = '\*'
# Aliases to export from this module
AliasesToExport = '\*'
# Private data to pass to the module specified in RootModule/ModuleToProcess. This may also contain a PSData hashtable with additional module metadata used by PowerShell.
PrivateData = @{
    PSData = @{
      # Tags applied to this module. These help with module discovery in online galleries.
      Tags = 'Tag1', 'Tag2', 'Tag-ModuleWithDependencies2-2.0'
      # A URL to the license for this module.
      LicenseUri = 'http://modulewithdependencies2.com/license'
      # A URL to the main website for this project.
      ProjectUri = 'http://modulewithdependencies2.com/'
      # A URL to an icon representing this module.
      IconUri = 'http://modulewithdependencies2.com/icon'
      # ReleaseNotes of this module
      ReleaseNotes = 'ModuleWithDependencies2 release notes'
    } # End of PSData hashtable
} # End of PrivateData hashtable
}
```


### <a name="external-dependencies"></a><span data-ttu-id="b96e1-130">Externí závislosti</span><span class="sxs-lookup"><span data-stu-id="b96e1-130">External dependencies</span></span>
<span data-ttu-id="b96e1-131">Několik závislostí modulu je možné spravovat externě, v takovém případě musí být přidaní do položky ExternalModuleDependencies v části PSData manifestu modulu.</span><span class="sxs-lookup"><span data-stu-id="b96e1-131">Some module dependencies can be managed externally, in that case they should be added to the ExternalModuleDependencies entry in the PSData section of the module manifest.</span></span>

<span data-ttu-id="b96e1-132">Pokud 'SnippetPx' není k dispozici v úložišti, níže chyba bude vyvolána.</span><span class="sxs-lookup"><span data-stu-id="b96e1-132">If 'SnippetPx' is not available on the repository, below error will be thrown.</span></span>
```powershell
Publish-PSArtifactUtility : PowerShellGet cannot resolve the module dependency 'SnippetPx' of the module 'TypePx' on the repository 'LocalRepo'. Verify that the dependent module 'SnippetPx' is available in the repository 'LocalRepo'. If this dependent 'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
```