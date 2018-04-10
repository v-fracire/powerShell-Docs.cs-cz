---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: Update-ModuleManifest
ms.openlocfilehash: 45f40f753af17e82c83dbf57dea13749ba626503
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="update-modulemanifest"></a><span data-ttu-id="7ecf1-103">Update-ModuleManifest</span><span class="sxs-lookup"><span data-stu-id="7ecf1-103">Update-ModuleManifest</span></span>
<span data-ttu-id="7ecf1-104">Aktualizuje soubor manifestu modulu.</span><span class="sxs-lookup"><span data-stu-id="7ecf1-104">Updates a module manifest file.</span></span>

## <a name="description"></a><span data-ttu-id="7ecf1-105">Popis</span><span class="sxs-lookup"><span data-stu-id="7ecf1-105">Description</span></span>

<span data-ttu-id="7ecf1-106">Rutinu Update-ModuleManifest aktualizací modulu souboru manifestu (.psd1).</span><span class="sxs-lookup"><span data-stu-id="7ecf1-106">The Update-ModuleManifest cmdlet updates a module manifest (.psd1) file.</span></span>

### <a name="notes"></a><span data-ttu-id="7ecf1-107">Poznámky</span><span class="sxs-lookup"><span data-stu-id="7ecf1-107">Notes</span></span>
    - <span data-ttu-id="7ecf1-108">DscResourcesToExport je podporována pouze na nejnovější rozhraní PowerShell verze 5.0.</span><span class="sxs-lookup"><span data-stu-id="7ecf1-108">DscResourcesToExport is only supported on the latest PowerShell version 5.0.</span></span> <span data-ttu-id="7ecf1-109">Jsme nebude možné aktualizovat pole, pokud používáte na nižší verze prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ecf1-109">We won’t be able to update the field if you are running on lower versions of PowerShell.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="7ecf1-110">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="7ecf1-110">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Update-ModuleManifest -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="7ecf1-111">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="7ecf1-111">Cmdlet online help reference</span></span>

[<span data-ttu-id="7ecf1-112">Update-ModuleManifest</span><span class="sxs-lookup"><span data-stu-id="7ecf1-112">Update-ModuleManifest</span></span>](http://go.microsoft.com/fwlink/?LinkId=619311)

## <a name="example-commands"></a><span data-ttu-id="7ecf1-113">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="7ecf1-113">Example commands</span></span>

<span data-ttu-id="7ecf1-114">Tato nová rutina se používá k aktualizace manifest souboru s hodnotami vstupní vlastnost nápovědy.</span><span class="sxs-lookup"><span data-stu-id="7ecf1-114">This new cmdlet is used to help update manifest file with input property values.</span></span> <span data-ttu-id="7ecf1-115">Všechny parametry, které nemá New-ModuleManifest trvá.</span><span class="sxs-lookup"><span data-stu-id="7ecf1-115">It takes all parameters that New-ModuleManifest does.</span></span>

<span data-ttu-id="7ecf1-116">Zjistíme, že mnoho modulu autoři chtěli zadejte "\*" exportovaný hodnoty, jako je například FunctionsToExport, CmdletsToExport, atd. Při publikování modulu v galerii prostředí PowerShell, neurčené funkce a příkazy se nenaplní správně do galerie.</span><span class="sxs-lookup"><span data-stu-id="7ecf1-116">We notice that a lot of module authors would like to specify “\*” in exported values such as FunctionsToExport, CmdletsToExport, etc. During module publishing to PowerShell Gallery, unspecified functions and commands will not be populated properly onto the Gallery.</span></span> <span data-ttu-id="7ecf1-117">Proto doporučujeme aktualizace modulu autoři jejich manifesty s správné hodnoty.</span><span class="sxs-lookup"><span data-stu-id="7ecf1-117">Therefore, we suggest module authors update their manifests with proper values.</span></span>

<span data-ttu-id="7ecf1-118">Pokud máte moduly, které byly exportovány vlastnosti, naplní aktualizace ModuleManifest zadaný soubor manifestu informace z exportovaných funkcí, rutin, proměnné atd:</span><span class="sxs-lookup"><span data-stu-id="7ecf1-118">If you have modules that have exported properties, Update-ModuleManifest will fill the specified manifest file with information from exported functions, cmdlets, variables etc:</span></span>
```powershell
Get-Content -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1"
@{
# Script module or binary module file associated with this manifest.
# RootModule = ''
# Version number of this module.
ModuleVersion = '2.5'
# ID used to uniquely identify this module
GUID = '610e5c5b-dc42-4eaa-8511-ebfb44066d5e'

#(Other properties removed here for Simplicity…)

# Functions to export from this module
FunctionsToExport = '*'
# Cmdlets to export from this module
CmdletsToExport = '*'
# Variables to export from this module
VariablesToExport = '*'
# Aliases to export from this module
AliasesToExport = '*'
}
```

<span data-ttu-id="7ecf1-119">Po aktualizaci ModuleManifest:</span><span class="sxs-lookup"><span data-stu-id="7ecf1-119">After Update-ModuleManifest:</span></span>
```powershell
Update-ModuleManifest -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1"
Get-Content -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1"
#
# Module manifest for module 'NewManifest'
#
# Generated by: author name
#
# Generated on: 11/13/2015
#
@{
# Script module or binary module file associated with this manifest.
# RootModule = ''
# Version number of this module.
ModuleVersion = '2.5'
# ID used to uniquely identify this module
GUID = '610e5c5b-dc42-4eaa-8511-ebfb44066d5e'
# Functions to export from this module
FunctionsToExport = 'Get-FooFn Get-FooWF'
# Cmdlets to export from this module
CmdletsToExport = 'Test-PSGetTestCmdlet'
}
```

<span data-ttu-id="7ecf1-120">Pro každý modul existují také pole metadat, které jsou s ním spojená.</span><span class="sxs-lookup"><span data-stu-id="7ecf1-120">For each module, there are also metadata fields associated with it.</span></span> <span data-ttu-id="7ecf1-121">Aby bylo možné zobrazit metadata správně na PowrShell galerie, můžete aktualizace ModuleManifest k naplnění těchto polí v rámci PrivateData.</span><span class="sxs-lookup"><span data-stu-id="7ecf1-121">In order to display metadata properly on PowrShell Gallery, you can use Update-ModuleManifest to populate those fields under PrivateData.</span></span>

```powershell
Update-ModuleManifest -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1" -Tags "Tag1" -LicenseUri "http://license.com" -ProjectUri "http://project.com" -IconUri "http://icon.com" -ReleaseNotes "Test module"
```

<span data-ttu-id="7ecf1-122">Zatřiďovací tabulky PrivateData ze souboru manifestu šablony má následující vlastnosti</span><span class="sxs-lookup"><span data-stu-id="7ecf1-122">PrivateData hashtable from the manifest file template has the following properties</span></span>

```powershell
# Private data to pass to the module specified in RootModule/ModuleToProcess. This may also contain a PSData hashtable with additional module metadata used by PowerShell.
PrivateData = @{
    PSData = @{
        # Tags applied to this module. These help with module discovery in online galleries.
        # Tags = @()

        # A URL to the license for this module.
        # LicenseUri = ''

        # A URL to the main website for this project.
        # ProjectUri = ''

        # A URL to an icon representing this module.
        # IconUri = ''

        # ReleaseNotes of this module
        # ReleaseNotes = ''

        # External dependent modules of this module
        # ExternalModuleDependencies = ''
    } # End of PSData hashtable
} # End of PrivateData hashtable
```