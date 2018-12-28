---
ms.date: 06/12/2017
contributor: manikb
keywords: Galerie prostředí powershell, rutina, psget
title: Moduly s kompatibilní edice Powershellu
ms.openlocfilehash: bda924393d37ea1596fbf0d813c10cbdea33c218
ms.sourcegitcommit: 548547b2d5fc73e726bb9fec6175d452a351d975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2018
ms.locfileid: "53655323"
---
# <a name="modules-with-compatible-powershell-editions"></a><span data-ttu-id="fa851-103">Moduly s kompatibilní edice Powershellu</span><span class="sxs-lookup"><span data-stu-id="fa851-103">Modules with compatible PowerShell Editions</span></span>

<span data-ttu-id="fa851-104">Od verze 5.1 je PowerShell k dispozici v různých edicích, které uvádějí různé sady funkcí a kompatibilitu platformy.</span><span class="sxs-lookup"><span data-stu-id="fa851-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="fa851-105">**Desktop Edition:** Založený na rozhraní .NET Framework a zajišťuje kompatibilitu se skripty a moduly cílenými na verze Powershellu spouštěné na plných edicích Windows, jako je jádro serveru a Windows Desktop.</span><span class="sxs-lookup"><span data-stu-id="fa851-105">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="fa851-106">**Core Edition:** Založená na prostředí .NET Core a zajišťuje kompatibilitu se skripty a moduly cílenými na verze Powershellu spouštěné na edicích Windows, jako je Nano Server a Windows IoT nízké nároky.</span><span class="sxs-lookup"><span data-stu-id="fa851-106">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

<span data-ttu-id="fa851-107">Verze powershellu je zobrazena ve vlastnosti PSEdition `$PSVersionTable`.</span><span class="sxs-lookup"><span data-stu-id="fa851-107">The running edition of PowerShell is shown in the PSEdition property of `$PSVersionTable`.</span></span>

```powershell
$PSVersionTable
```

```output
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

## <a name="declaring-compatible-editions"></a><span data-ttu-id="fa851-108">Deklarování kompatibilní edice</span><span class="sxs-lookup"><span data-stu-id="fa851-108">Declaring compatible editions</span></span>

<span data-ttu-id="fa851-109">Autoři modulu mají možnost deklarovat své moduly jako kompatibilní s jednou nebo více edicemi PowerShellu, které používají klíč manifestu CompatiblePSEditions.</span><span class="sxs-lookup"><span data-stu-id="fa851-109">Module authors can declare their modules to be compatible with one or more PowerShell editions using the CompatiblePSEditions module manifest key.</span></span> <span data-ttu-id="fa851-110">Podporu tohoto klíče poskytují jenom prostředí PowerShell 5.1 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="fa851-110">This key is only supported on PowerShell 5.1 or later.</span></span>

> [!NOTE]
> <span data-ttu-id="fa851-111">Jakmile modul manifestu je zadán s klíčem CompatiblePSEditions, nelze importovat na nižší verzi prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa851-111">Once a module manifest is specified with the CompatiblePSEditions key, it can not be imported on lower versions of PowerShell.</span></span>

```powershell
New-ModuleManifest -Path .\TestModuleWithEdition.psd1 -CompatiblePSEditions Desktop,Core -PowerShellVersion 5.1
$ModuleInfo = Test-ModuleManifest -Path .\TestModuleWithEdition.psd1
$ModuleInfo.CompatiblePSEditions
```

```output
Desktop
Core
```

```powershell
$ModuleInfo | Get-Member CompatiblePSEditions
```

```output
   TypeName: System.Management.Automation.PSModuleInfo

Name                 MemberType Definition
----                 ---------- ----------
CompatiblePSEditions Property   System.Collections.Generic.IEnumerable[string] CompatiblePSEditions {get;}
```

<span data-ttu-id="fa851-112">Při získávání seznamu dostupných modulů můžete filtrovat seznam podle edice PowerShellu.</span><span class="sxs-lookup"><span data-stu-id="fa851-112">When getting a list of available modules, you can filter the list by PowerShell edition.</span></span>

```powershell
Get-Module -ListAvailable -PSEdition Desktop
```

```output
    Directory: C:\Program Files\WindowsPowerShell\Modules


ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   1.0        ModuleWithPSEditions
```

```powershell
Get-Module -ListAvailable -PSEdition Core | % CompatiblePSEditions
```

```output
Desktop
Core
```

## <a name="targeting-multiple-editions"></a><span data-ttu-id="fa851-113">Cílení na více verzí</span><span class="sxs-lookup"><span data-stu-id="fa851-113">Targeting multiple editions</span></span>

<span data-ttu-id="fa851-114">Autoři modulu můžete publikovat v modulu single cílení jednoho nebo obou edice Powershellu (v desktopové i Core).</span><span class="sxs-lookup"><span data-stu-id="fa851-114">Module authors can publish a single module targeting to either or both PowerShell editions (Desktop and Core).</span></span>

<span data-ttu-id="fa851-115">Jeden modul mohl pracovat na ploše a jádra edice, v tomto modulu má autor přidat požadované logiku v obou RootModule, nebo v manifestu modulu pomocí $PSEdition proměnné.</span><span class="sxs-lookup"><span data-stu-id="fa851-115">A single module can work on both Desktop and Core editions, in that module author has to add required logic in either RootModule or in the module manifest using $PSEdition variable.</span></span> <span data-ttu-id="fa851-116">Moduly může mít dvě sady na CoreCLR a FullCLR zkompilované knihovny DLL.</span><span class="sxs-lookup"><span data-stu-id="fa851-116">Modules can have two sets of compiled DLLs targeting both CoreCLR and FullCLR.</span></span> <span data-ttu-id="fa851-117">Tady je několik možností pro balíček modulu s logiku pro načítání knihoven DLL správné.</span><span class="sxs-lookup"><span data-stu-id="fa851-117">Here are the couple of options to package your module with logic for loading proper dlls.</span></span>

### <a name="option-1-packaging-a-module-for-targeting-multiple-versions-and-multiple-editions-of-powershell"></a><span data-ttu-id="fa851-118">Možnost 1: Vytvoření balíčku modulu pro cílení na více verzí a více edicemi Powershellu</span><span class="sxs-lookup"><span data-stu-id="fa851-118">Option 1: Packaging a module for targeting multiple versions and multiple editions of PowerShell</span></span>

<span data-ttu-id="fa851-119">Obsah složky modulu</span><span class="sxs-lookup"><span data-stu-id="fa851-119">Module folder contents</span></span>

- <span data-ttu-id="fa851-120">Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="fa851-120">Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="fa851-121">Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="fa851-121">Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="fa851-122">PSScriptAnalyzer.psd1</span><span class="sxs-lookup"><span data-stu-id="fa851-122">PSScriptAnalyzer.psd1</span></span>
- <span data-ttu-id="fa851-123">PSScriptAnalyzer.psm1</span><span class="sxs-lookup"><span data-stu-id="fa851-123">PSScriptAnalyzer.psm1</span></span>
- <span data-ttu-id="fa851-124">ScriptAnalyzer.format.ps1xml</span><span class="sxs-lookup"><span data-stu-id="fa851-124">ScriptAnalyzer.format.ps1xml</span></span>
- <span data-ttu-id="fa851-125">ScriptAnalyzer.types.ps1xml</span><span class="sxs-lookup"><span data-stu-id="fa851-125">ScriptAnalyzer.types.ps1xml</span></span>
- <span data-ttu-id="fa851-126">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="fa851-126">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="fa851-127">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="fa851-127">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="fa851-128">en-US\about_PSScriptAnalyzer.help.txt</span><span class="sxs-lookup"><span data-stu-id="fa851-128">en-US\about_PSScriptAnalyzer.help.txt</span></span>
- <span data-ttu-id="fa851-129">en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml</span><span class="sxs-lookup"><span data-stu-id="fa851-129">en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml</span></span>
- <span data-ttu-id="fa851-130">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="fa851-130">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="fa851-131">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="fa851-131">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="fa851-132">Settings\CmdletDesign.psd1</span><span class="sxs-lookup"><span data-stu-id="fa851-132">Settings\CmdletDesign.psd1</span></span>
- <span data-ttu-id="fa851-133">Settings\DSC.psd1</span><span class="sxs-lookup"><span data-stu-id="fa851-133">Settings\DSC.psd1</span></span>
- <span data-ttu-id="fa851-134">Settings\ScriptFunctions.psd1</span><span class="sxs-lookup"><span data-stu-id="fa851-134">Settings\ScriptFunctions.psd1</span></span>
- <span data-ttu-id="fa851-135">Settings\ScriptingStyle.psd1</span><span class="sxs-lookup"><span data-stu-id="fa851-135">Settings\ScriptingStyle.psd1</span></span>
- <span data-ttu-id="fa851-136">Settings\ScriptSecurity.psd1</span><span class="sxs-lookup"><span data-stu-id="fa851-136">Settings\ScriptSecurity.psd1</span></span>

<span data-ttu-id="fa851-137">Obsah souboru PSScriptAnalyzer.psd1</span><span class="sxs-lookup"><span data-stu-id="fa851-137">Contents of PSScriptAnalyzer.psd1 file</span></span>

```powershell
@{

# Author of this module
Author = 'Microsoft Corporation'

# Script module or binary module file associated with this manifest.
RootModule = 'PSScriptAnalyzer.psm1'

# Version number of this module.
ModuleVersion = '1.6.1'

# ---
}
```

<span data-ttu-id="fa851-138">Pod logiky načte požadované sestavení v závislosti na aktuální edici nebo verzi.</span><span class="sxs-lookup"><span data-stu-id="fa851-138">Below logic loads the required assemblies depending on the current edition or version.</span></span>

<span data-ttu-id="fa851-139">Obsah souboru PSScriptAnalyzer.psm1:</span><span class="sxs-lookup"><span data-stu-id="fa851-139">Contents of PSScriptAnalyzer.psm1 file:</span></span>

```powershell
#
# Script module for module 'PSScriptAnalyzer'
#
Set-StrictMode -Version Latest

# Set up some helper variables to make it easier to work with the module
$PSModule = $ExecutionContext.SessionState.Module
$PSModuleRoot = $PSModule.ModuleBase

# Import the appropriate nested binary module based on the current PowerShell version
$binaryModuleRoot = $PSModuleRoot


if (($PSVersionTable.Keys -contains "PSEdition") -and ($PSVersionTable.PSEdition -ne 'Desktop')) {
    $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'coreclr'
}
else
{
    if ($PSVersionTable.PSVersion -lt [Version]'5.0')
    {
        $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'PSv3'
    }
}

$binaryModulePath = Join-Path -Path $binaryModuleRoot -ChildPath 'Microsoft.Windows.PowerShell.ScriptAnalyzer.dll'
$binaryModule = Import-Module -Name $binaryModulePath -PassThru

# When the module is unloaded, remove the nested binary module that was loaded with it
$PSModule.OnRemove = {
    Remove-Module -ModuleInfo $binaryModule
}
```

### <a name="option-2-use-psedition-variable-in-the-psd1-file-to-load-the-proper-dlls-and-nestedrequired-modules"></a><span data-ttu-id="fa851-140">Možnost 2: Pomocí proměnné $PSEdition v soubor PSD1 načíst správné knihovny DLL a vnořené/požadované moduly</span><span class="sxs-lookup"><span data-stu-id="fa851-140">Option 2: Use $PSEdition variable in the PSD1 file to load the proper DLLs and Nested/Required modules</span></span>

<span data-ttu-id="fa851-141">PS 5.1 nebo novější je v souboru manifestu modulu povolen $PSEdition globální proměnné.</span><span class="sxs-lookup"><span data-stu-id="fa851-141">In PS 5.1 or newer, $PSEdition global variable is allowed in the module manifest file.</span></span> <span data-ttu-id="fa851-142">Pomocí této proměnné, Autor modulu můžete určit podmíněného hodnoty v souboru manifestu modulu.</span><span class="sxs-lookup"><span data-stu-id="fa851-142">Using this variable, module author can specify the conditional values in the module manifest file.</span></span> <span data-ttu-id="fa851-143">$PSEdition proměnné může být odkazováno v režimu s omezeným přístupem jazyka nebo datové části.</span><span class="sxs-lookup"><span data-stu-id="fa851-143">$PSEdition variable can be referenced in restricted language mode or a Data section.</span></span>

> [!NOTE]
> <span data-ttu-id="fa851-144">Jakmile modul manifestu je zadán s parametrem CompatiblePSEditions klíč nebo používá `$PSEdition` proměnné, nelze jej importovat na nižší verzi prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa851-144">Once a module manifest is specified with the CompatiblePSEditions key or uses `$PSEdition` variable, it can not be imported on lower versions of PowerShell.</span></span>

<span data-ttu-id="fa851-145">Ukázkový soubor manifestu modulu s klíčem CompatiblePSEditions</span><span class="sxs-lookup"><span data-stu-id="fa851-145">Sample module manifest file with CompatiblePSEditions key</span></span>

```powershell
@{
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
}
```

### <a name="module-contents"></a><span data-ttu-id="fa851-146">Obsah modulu</span><span class="sxs-lookup"><span data-stu-id="fa851-146">Module contents</span></span>

```powershell
dir -Recurse
```

```output
    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions

Mode           LastWriteTime   Length Name
----           -------------   ------ ----
d-----    7/5/2016   1:37 PM          clr
d-----    7/5/2016   1:36 PM          coreclr
-a----    7/5/2016   1:34 PM     4906 ModuleWithEditions.psd1

    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\clr

Mode           LastWriteTime    Length Name
----           -------------    ------ ----
-a----    7/5/2016   1:35 PM         0 MyFullClrNM1.dll
-a----    7/5/2016   1:35 PM         0 MyFullClrNM2.dll
-a----    7/5/2016   1:35 PM         0 MyFullClrRM.dl

    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\coreclr

Mode           LastWriteTime   Length Name
----           -------------   ------ ----
-a----    7/5/2016   1:35 PM        0 MyCoreClrNM1.dll
-a----    7/5/2016   1:35 PM        0 MyCoreClrNM2.dll
-a----    7/5/2016   1:35 PM        0 MyCoreClrRM.dl
```

<span data-ttu-id="fa851-147">Galerie prostředí PowerShell uživatelé najdou seznam modulů, které jsou podporovány na konkrétní edici Powershellu pomocí značek PSEdition_Desktop a PSEdition_Core.</span><span class="sxs-lookup"><span data-stu-id="fa851-147">PowerShell Gallery users can find the list of modules supported on a specific PowerShell Edition using tags PSEdition_Desktop and PSEdition_Core.</span></span>

<span data-ttu-id="fa851-148">Moduly bez PSEdition_Desktop a PSEdition_Core značek jsou považovány za fungovat bez problémů na edice Powershellu Desktop.</span><span class="sxs-lookup"><span data-stu-id="fa851-148">Modules without PSEdition_Desktop and PSEdition_Core tags are considered to work fine on PowerShell Desktop editions.</span></span>

```powershell
# Find modules supported on PowerShell Desktop edition
Find-Module -Tag PSEdition_Desktop

# Find modules supported on PowerShell Core editions
Find-Module -Tag PSEdition_Core
```

## <a name="more-details"></a><span data-ttu-id="fa851-149">Další podrobnosti</span><span class="sxs-lookup"><span data-stu-id="fa851-149">More details</span></span>

[<span data-ttu-id="fa851-150">Skripty s PSEditions</span><span class="sxs-lookup"><span data-stu-id="fa851-150">Scripts with PSEditions</span></span>](script-psedition-support.md)

[<span data-ttu-id="fa851-151">Podpora PSEditions na PowerShellGallery</span><span class="sxs-lookup"><span data-stu-id="fa851-151">PSEditions support on PowerShellGallery</span></span>](../how-to/finding-packages/searching-by-compatibility.md)

[<span data-ttu-id="fa851-152">Aktualizace manifestu modulu</span><span class="sxs-lookup"><span data-stu-id="fa851-152">Update module manifest</span></span>](/powershell/module/powershellget/update-modulemanifest)
