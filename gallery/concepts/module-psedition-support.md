---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: Galerie prostředí powershell, rutiny, psget
title: Moduly s kompatibilní verze prostředí PowerShell
ms.openlocfilehash: 631314e63e49723b3c393c8d8c20de9a297027fb
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="modules-with-compatible-powershell-editions"></a><span data-ttu-id="c21a1-103">Moduly s kompatibilní verze prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="c21a1-103">Modules with compatible PowerShell Editions</span></span>

<span data-ttu-id="c21a1-104">Od verze 5.1 je PowerShell k dispozici v různých edicích, které uvádějí různé sady funkcí a kompatibilitu platformy.</span><span class="sxs-lookup"><span data-stu-id="c21a1-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="c21a1-105">**Desktop Edition:** Tato edice je založená na rozhraní .NET Framework a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na plných edicích Windows, jako je Jádro serveru a Windows Desktop.</span><span class="sxs-lookup"><span data-stu-id="c21a1-105">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="c21a1-106">**Core Edition:** Tato edice je založená na rozhraní .NET Core a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na edicích Windows s nízkými nároky na prostředky, jako je Nano Server a Windows IoT.</span><span class="sxs-lookup"><span data-stu-id="c21a1-106">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

## <a name="the-running-edition-of-powershell-is-shown-in-the-psedition-property-of-psversiontable"></a><span data-ttu-id="c21a1-107">Používaná verze PowerShellu je uvedena ve vlastnosti PSEdition parametru $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="c21a1-107">The running edition of PowerShell is shown in the PSEdition property of $PSVersionTable.</span></span>

```powershell
$PSVersionTable

Name                           Value
----                           -----
PSVersion                      5.1.14300.1000
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
CLRVersion                     4.0.30319.42000
BuildVersion                   10.0.14300.1000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

## <a name="module-authors-can-declare-their-modules-to-be-compatible-with-one-or-more-powershell-editions-using-the-compatiblepseditions-module-manifest-key-this-key-is-only-supported-on-powershell-51-or-later"></a><span data-ttu-id="c21a1-108">Autoři modulu mají možnost deklarovat své moduly jako kompatibilní s jednou nebo více edicemi PowerShellu, které používají klíč manifestu CompatiblePSEditions.</span><span class="sxs-lookup"><span data-stu-id="c21a1-108">Module authors can declare their modules to be compatible with one or more PowerShell editions using the CompatiblePSEditions module manifest key.</span></span> <span data-ttu-id="c21a1-109">Podporu tohoto klíče poskytují jenom prostředí PowerShell 5.1 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="c21a1-109">This key is only supported on PowerShell 5.1 or later.</span></span>

<span data-ttu-id="c21a1-110">*Poznámka:* po modul manifestu je zadaný klíč CompatiblePSEditions, nelze jej importovat na nižší verze prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c21a1-110">*NOTE* Once a module manifest is specified with the CompatiblePSEditions key, it can not be imported on lower versions of PowerShell.</span></span>

```powershell
New-ModuleManifest -Path .\TestModuleWithEdition.psd1 -CompatiblePSEditions Desktop,Core -PowerShellVersion 5.1
$ModuleInfo = Test-ModuleManifest -Path .\TestModuleWithEdition.psd1
$ModuleInfo.CompatiblePSEditions
Desktop
Core

$ModuleInfo | Get-Member CompatiblePSEditions

   TypeName: System.Management.Automation.PSModuleInfo

Name                 MemberType Definition
----                 ---------- ----------
CompatiblePSEditions Property   System.Collections.Generic.IEnumerable[string] CompatiblePSEditions {get;}

```

<span data-ttu-id="c21a1-111">Při získávání seznamu dostupných modulů můžete filtrovat seznam podle edice PowerShellu.</span><span class="sxs-lookup"><span data-stu-id="c21a1-111">When getting a list of available modules, you can filter the list by PowerShell edition.</span></span>

```powershell
Get-Module -ListAvailable -PSEdition Desktop

    Directory: C:\Program Files\WindowsPowerShell\Modules


ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   1.0        ModuleWithPSEditions

Get-Module -ListAvailable -PSEdition Core | % CompatiblePSEditions
Desktop
Core

```

## <a name="module-authors-can-publish-a-single-module-targeting-to-either-or-both-powershell-editions-desktop-and-core"></a><span data-ttu-id="c21a1-112">Autoři modulu můžete publikovat v modulu single cílení na obojím prostředí PowerShell edice (Desktop a jader)</span><span class="sxs-lookup"><span data-stu-id="c21a1-112">Module authors can publish a single module targeting to either or both PowerShell editions (Desktop and Core)</span></span>

<span data-ttu-id="c21a1-113">Jeden modul může pracovat na ploše a základní verze, v tomto modulu má autor přidat požadované logiku v buď RootModule nebo v manifestu modulu pomocí $PSEdition proměnné.</span><span class="sxs-lookup"><span data-stu-id="c21a1-113">A single module can work on both Desktop and Core editions, in that module author has to add required logic in either RootModule or in the module manifest using $PSEdition variable.</span></span>
<span data-ttu-id="c21a1-114">Moduly může mít dvě sady cílené na CoreCLR a FullCLR zkompilované knihovny DLL.</span><span class="sxs-lookup"><span data-stu-id="c21a1-114">Modules can have two sets of compiled DLLs targeting both CoreCLR and FullCLR.</span></span>
<span data-ttu-id="c21a1-115">Tady je několik možností balíček modulu s logiku pro načítání knihoven DLL správné.</span><span class="sxs-lookup"><span data-stu-id="c21a1-115">Here are the couple of options to package your module with logic for loading proper dlls.</span></span>

### <a name="option-1-packaging-a-module-for-targeting-multiple-versions-and-multiple-editions-of-powershell"></a><span data-ttu-id="c21a1-116">Možnost 1: Zabalení modul pro cílení na více verzí a víc edicí prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="c21a1-116">Option 1: Packaging a module for targeting multiple versions and multiple editions of PowerShell</span></span>

#### <a name="module-folder-contents"></a><span data-ttu-id="c21a1-117">Obsah složky modulu</span><span class="sxs-lookup"><span data-stu-id="c21a1-117">Module folder contents</span></span>

- <span data-ttu-id="c21a1-118">Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="c21a1-118">Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="c21a1-119">Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="c21a1-119">Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="c21a1-120">PSScriptAnalyzer.psd1</span><span class="sxs-lookup"><span data-stu-id="c21a1-120">PSScriptAnalyzer.psd1</span></span>
- <span data-ttu-id="c21a1-121">PSScriptAnalyzer.psm1</span><span class="sxs-lookup"><span data-stu-id="c21a1-121">PSScriptAnalyzer.psm1</span></span>
- <span data-ttu-id="c21a1-122">ScriptAnalyzer.format.ps1xml</span><span class="sxs-lookup"><span data-stu-id="c21a1-122">ScriptAnalyzer.format.ps1xml</span></span>
- <span data-ttu-id="c21a1-123">ScriptAnalyzer.types.ps1xml</span><span class="sxs-lookup"><span data-stu-id="c21a1-123">ScriptAnalyzer.types.ps1xml</span></span>
- <span data-ttu-id="c21a1-124">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="c21a1-124">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="c21a1-125">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="c21a1-125">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="c21a1-126">en-US\about_PSScriptAnalyzer.help.txt</span><span class="sxs-lookup"><span data-stu-id="c21a1-126">en-US\about_PSScriptAnalyzer.help.txt</span></span>
- <span data-ttu-id="c21a1-127">en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml</span><span class="sxs-lookup"><span data-stu-id="c21a1-127">en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml</span></span>
- <span data-ttu-id="c21a1-128">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="c21a1-128">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="c21a1-129">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="c21a1-129">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="c21a1-130">Settings\CmdletDesign.psd1</span><span class="sxs-lookup"><span data-stu-id="c21a1-130">Settings\CmdletDesign.psd1</span></span>
- <span data-ttu-id="c21a1-131">Settings\DSC.psd1</span><span class="sxs-lookup"><span data-stu-id="c21a1-131">Settings\DSC.psd1</span></span>
- <span data-ttu-id="c21a1-132">Settings\ScriptFunctions.psd1</span><span class="sxs-lookup"><span data-stu-id="c21a1-132">Settings\ScriptFunctions.psd1</span></span>
- <span data-ttu-id="c21a1-133">Settings\ScriptingStyle.psd1</span><span class="sxs-lookup"><span data-stu-id="c21a1-133">Settings\ScriptingStyle.psd1</span></span>
- <span data-ttu-id="c21a1-134">Settings\ScriptSecurity.psd1</span><span class="sxs-lookup"><span data-stu-id="c21a1-134">Settings\ScriptSecurity.psd1</span></span>

#### <a name="contents-of-psscriptanalyzerpsd1-file"></a><span data-ttu-id="c21a1-135">Obsah souboru PSScriptAnalyzer.psd1</span><span class="sxs-lookup"><span data-stu-id="c21a1-135">Contents of PSScriptAnalyzer.psd1 file</span></span>

```powershell
@{

# Author of this module
Author = 'Microsoft Corporation'

# Script module or binary module file associated with this manifest.
RootModule = 'PSScriptAnalyzer.psm1'

# Version number of this module.
ModuleVersion = '1.6.1'

# ---
}
```

#### <a name="contents-of-psscriptanalyzerpsm1-file"></a><span data-ttu-id="c21a1-136">Obsah souboru PSScriptAnalyzer.psm1</span><span class="sxs-lookup"><span data-stu-id="c21a1-136">Contents of PSScriptAnalyzer.psm1 file</span></span>

<span data-ttu-id="c21a1-137">Níže logiku načte požadovaná sestavení v závislosti na aktuální edice nebo verze.</span><span class="sxs-lookup"><span data-stu-id="c21a1-137">Below logic loads the required assemblies depending on the current edition or version.</span></span>

```powershell
#
# Script module for module 'PSScriptAnalyzer'
#
Set-StrictMode -Version Latest

# Set up some helper variables to make it easier to work with the module
$PSModule = $ExecutionContext.SessionState.Module
$PSModuleRoot = $PSModule.ModuleBase

# Import the appropriate nested binary module based on the current PowerShell version
$binaryModuleRoot = $PSModuleRoot


if (($PSVersionTable.Keys -contains "PSEdition") -and ($PSVersionTable.PSEdition -ne 'Desktop')) {
    $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'coreclr'
}
else
{
    if ($PSVersionTable.PSVersion -lt [Version]'5.0') {
        $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'PSv3'
    }
}

$binaryModulePath = Join-Path -Path $binaryModuleRoot -ChildPath 'Microsoft.Windows.PowerShell.ScriptAnalyzer.dll'
$binaryModule = Import-Module -Name $binaryModulePath -PassThru

# When the module is unloaded, remove the nested binary module that was loaded with it
$PSModule.OnRemove = {
    Remove-Module -ModuleInfo $binaryModule
}

```

### <a name="option-2-use-psedition-variable-in-the-psd1-file-to-load-the-proper-dlls-and-nestedrequired-modules"></a><span data-ttu-id="c21a1-138">Možnost 2: Použijte proměnnou $PSEdition v soubor PSD1 načíst správné knihovny DLL a vnořené/požadované moduly</span><span class="sxs-lookup"><span data-stu-id="c21a1-138">Option 2: Use $PSEdition variable in the PSD1 file to load the proper DLLs and Nested/Required modules</span></span>

<span data-ttu-id="c21a1-139">V PS 5.1 nebo novější $PSEdition – globální proměnná je povolena v souboru manifestu modulu.</span><span class="sxs-lookup"><span data-stu-id="c21a1-139">In PS 5.1 or newer, $PSEdition global variable is allowed in the module manifest file.</span></span>
<span data-ttu-id="c21a1-140">Pomocí této proměnné, Autor modulu můžete zadat podmíněného hodnoty v souboru manifestu modulu.</span><span class="sxs-lookup"><span data-stu-id="c21a1-140">Using this variable, module author can specify the conditional values in the module manifest file.</span></span> <span data-ttu-id="c21a1-141">$PSEdition proměnná může být odkaz v režimu s omezeným přístupem jazyk nebo datové části.</span><span class="sxs-lookup"><span data-stu-id="c21a1-141">$PSEdition variable can be referenced in restricted language mode or a Data section.</span></span>

<span data-ttu-id="c21a1-142">*Poznámka:* po modul manifestu je zadán s klíčem CompatiblePSEditions nebo používá proměnnou $PSEdition, nelze jej importovat na nižší verze prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c21a1-142">*NOTE* Once a module manifest is specified with the CompatiblePSEditions key or uses $PSEdition variable, it can not be imported on lower versions of PowerShell.</span></span>


#### <a name="sample-module-manifest-file-with-compatiblepseditions-key"></a><span data-ttu-id="c21a1-143">Ukázku souboru manifestu modulu klíčem CompatiblePSEditions</span><span class="sxs-lookup"><span data-stu-id="c21a1-143">Sample module manifest file with CompatiblePSEditions key</span></span>

```powershell
@{
# - - -

# Script module or binary module file associated with this manifest.
RootModule = if($PSEdition -eq 'Core')
{
'coreclr\MyCoreClrRM.dll'
}
else # Desktop
{
'clr\MyFullClrRM.dll'
}

# Supported PSEditions
CompatiblePSEditions = 'Desktop', 'Core'

# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
NestedModules = if($PSEdition -eq 'Core')
{
'coreclr\MyCoreClrNM1.dll',
'coreclr\MyCoreClrNM2.dll'
}
else # Desktop
{
'clr\MyFullClrNM1.dll',
'clr\MyFullClrNM2.dll'
}

# -- - -
}
```

#### <a name="module-contents"></a><span data-ttu-id="c21a1-144">Obsah modulu</span><span class="sxs-lookup"><span data-stu-id="c21a1-144">Module contents</span></span>

```powershell

PS C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions> dir -Recurse

    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         7/5/2016   1:37 PM                clr
d-----         7/5/2016   1:36 PM                coreclr
-a----         7/5/2016   1:34 PM           4906 ModuleWithEditions.psd1

    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\clr

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         7/5/2016   1:35 PM              0 MyFullClrNM1.dll
-a----         7/5/2016   1:35 PM              0 MyFullClrNM2.dll
-a----         7/5/2016   1:35 PM              0 MyFullClrRM.dl

    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\coreclr

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         7/5/2016   1:35 PM              0 MyCoreClrNM1.dll
-a----         7/5/2016   1:35 PM              0 MyCoreClrNM2.dll
-a----         7/5/2016   1:35 PM              0 MyCoreClrRM.dl
```

## <a name="powershell-gallery-users-can-find-the-list-of-modules-supported-on-a-specific-powershell-edition-using-tags-pseditiondesktop-and-pseditioncore"></a><span data-ttu-id="c21a1-145">Galerie prostředí PowerShell můžou uživatelé najít seznamu modulů, které jsou podporovány na konkrétní verzi prostředí PowerShell pomocí značek PSEdition_Desktop a PSEdition_Core.</span><span class="sxs-lookup"><span data-stu-id="c21a1-145">PowerShell Gallery users can find the list of modules supported on a specific PowerShell Edition using tags PSEdition_Desktop and PSEdition_Core.</span></span>

<span data-ttu-id="c21a1-146">Moduly bez PSEdition_Desktop a PSEdition_Core značky jsou považovány za bez problémů fungují na edice Desktop prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c21a1-146">Modules without PSEdition_Desktop and PSEdition_Core tags are considered to work fine on PowerShell Desktop editions.</span></span>

```powershell

# Find modules supported on PowerShell Desktop edition
Find-Module -Tag PSEdition_Desktop

# Find modules supported on PowerShell Core editions
Find-Module -Tag PSEdition_Core

```


## <a name="more-details"></a><span data-ttu-id="c21a1-147">Další informace</span><span class="sxs-lookup"><span data-stu-id="c21a1-147">More details</span></span>

- [<span data-ttu-id="c21a1-148">Skripty s PSEditions</span><span class="sxs-lookup"><span data-stu-id="c21a1-148">Scripts with PSEditions</span></span>](script-psedition-support.md)
- [<span data-ttu-id="c21a1-149">Podpora PSEditions na PowerShellGallery</span><span class="sxs-lookup"><span data-stu-id="c21a1-149">PSEditions support on PowerShellGallery</span></span>](../how-to/finding-items/searching-by-psedition.md)
- <span data-ttu-id="c21a1-150">[Aktualizace modulu manifest] (/ prostředí powershell nebo modul/powershellget/update-modulemanifest)</span><span class="sxs-lookup"><span data-stu-id="c21a1-150">[Update module manifest] (/powershell/module/powershellget/update-modulemanifest)</span></span>