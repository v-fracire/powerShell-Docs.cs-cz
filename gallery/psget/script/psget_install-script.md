---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: "Instalační skript"
ms.openlocfilehash: 9ce4125329ea2a38f27f9305b169c7fcf3e9df42
ms.sourcegitcommit: 58371abe9db4b9a0e4e1eb82d39a9f9e187355f9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/05/2017
---
# <a name="install-script"></a><span data-ttu-id="cc3df-103">Instalační skript</span><span class="sxs-lookup"><span data-stu-id="cc3df-103">Install-Script</span></span>

<span data-ttu-id="cc3df-104">Nainstaluje soubory skriptu prostředí PowerShell z online úložiště na místním počítači.</span><span class="sxs-lookup"><span data-stu-id="cc3df-104">Installs the PowerShell script files from online repositories to the local computer.</span></span>

## <a name="description"></a><span data-ttu-id="cc3df-105">Popis</span><span class="sxs-lookup"><span data-stu-id="cc3df-105">Description</span></span>

<span data-ttu-id="cc3df-106">Instalační skript rutiny vyhledá a stáhne jeden nebo více skriptů z online galerie, ověří a nainstaluje je do oboru zadanou instalaci místního počítače.</span><span class="sxs-lookup"><span data-stu-id="cc3df-106">The Install-Script cmdlet finds and downloads one or more scripts from an online gallery, validates and installs them on the local computer to the specified installation scope.</span></span>

<span data-ttu-id="cc3df-107">Pokud je definován žádný obor, nebo pokud je hodnota parametru oboru AllUsers, skript se nainstaluje do %systemdrive%:\Program Files\WindowsPowerShell\scripts.</span><span class="sxs-lookup"><span data-stu-id="cc3df-107">When no scope is defined, or when the value of the Scope parameter is AllUsers, the script is installed to %systemdrive%:\Program Files\WindowsPowerShell\scripts.</span></span> <span data-ttu-id="cc3df-108">Pokud je hodnota oboru CurrentUser, skript se nainstaluje do $home\Documents\WindowsPowerShell\scripts.</span><span class="sxs-lookup"><span data-stu-id="cc3df-108">When the value of Scope is CurrentUser, the script is installed to $home\Documents\WindowsPowerShell\scripts.</span></span>

<span data-ttu-id="cc3df-109">Můžete filtrovat výsledky podle minimální a přesné verze zadané skriptů.</span><span class="sxs-lookup"><span data-stu-id="cc3df-109">You can filter your results based on minimum and exact versions of specified scripts.</span></span>

<span data-ttu-id="cc3df-110">Některé důležité poznámky:</span><span class="sxs-lookup"><span data-stu-id="cc3df-110">Some important notes:</span></span>
- <span data-ttu-id="cc3df-111">Skripty jsou nainstalované jeden soubory.</span><span class="sxs-lookup"><span data-stu-id="cc3df-111">Scripts are installed single files.</span></span> <span data-ttu-id="cc3df-112">V důsledku toho je nainstalována pouze jedna kopie skriptu a více verzí skripty nemůže být nainstalované-souběžného v systému.</span><span class="sxs-lookup"><span data-stu-id="cc3df-112">As a result, only one copy of a script is installed, and multiple versions of scripts cannot be installed side-by-side on a system.</span></span> 
- <span data-ttu-id="cc3df-113">Skripty může definovat závislosti na externí moduly, které se nainstalují při spuštění instalační skript.</span><span class="sxs-lookup"><span data-stu-id="cc3df-113">Scripts may define dependencies on external modules, which will  be installed when Install-Script is run.</span></span>
- <span data-ttu-id="cc3df-114">**Nedůvěryhodná zeptat:** přijetí uživateli je požadováno pro instalaci skripty z nedůvěryhodné úložiště.</span><span class="sxs-lookup"><span data-stu-id="cc3df-114">**Untrusted prompt:** User acceptance is required for installing the scripts from an untrusted repository.</span></span>
- <span data-ttu-id="cc3df-115">RequiredVersion nainstaluje zadaná verze v SxS s existující verze na rozhraní PowerShell verze 5.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="cc3df-115">RequiredVersion installs the specified version in SxS with existing versions on PowerShell version 5.0 or newer.</span></span>

<span data-ttu-id="cc3df-116">Zástupné znaky nejsou podporovány v - názvu na instalační skript, Uložit skript a odinstalační skript rutiny.</span><span class="sxs-lookup"><span data-stu-id="cc3df-116">Wildcards are not supported in -Name on Install-Script, Save-Script, and Uninstall-Script cmdlets.</span></span>

### <a name="scope"></a><span data-ttu-id="cc3df-117">Obor</span><span class="sxs-lookup"><span data-stu-id="cc3df-117">Scope</span></span>
<span data-ttu-id="cc3df-118">Určuje obor instalace skriptu.</span><span class="sxs-lookup"><span data-stu-id="cc3df-118">Specifies the installation scope of the script.</span></span> <span data-ttu-id="cc3df-119">Přípustné hodnoty tohoto parametru jsou: AllUsers a CurrentUser.</span><span class="sxs-lookup"><span data-stu-id="cc3df-119">The acceptable values for this parameter are: AllUsers and CurrentUser.</span></span>

<span data-ttu-id="cc3df-120">Výchozí instalace obor je AllUsers.</span><span class="sxs-lookup"><span data-stu-id="cc3df-120">The default installation scope is AllUsers.</span></span>

<span data-ttu-id="cc3df-121">Oboru AllUsers umožňuje skriptů nainstalovat do umístění, které je přístupné pro všechny uživatele počítače, který je "$env: SystemDrive\Program Files\WindowsPowerShell\scripts".</span><span class="sxs-lookup"><span data-stu-id="cc3df-121">The AllUsers scope lets scripts be installed in a location that is accessible to all users of the computer, that is, "$env:SystemDrive\Program Files\WindowsPowerShell\scripts".</span></span>

<span data-ttu-id="cc3df-122">Oboru CurrentUser umožňuje nainstalovat jenom na "$home\Documents\WindowsPowerShell\scripts", skripty tak, aby tento skript je k dispozici pouze pro aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="cc3df-122">The CurrentUser scope lets scripts be installed only to "$home\Documents\WindowsPowerShell\scripts", so that the script is available only to the current user.</span></span>


<span data-ttu-id="cc3df-123">Určuje obor instalace skriptu.</span><span class="sxs-lookup"><span data-stu-id="cc3df-123">Specifies the installation scope of the script.</span></span> <span data-ttu-id="cc3df-124">Platné hodnoty jsou: AllUsers a CurrentUser.</span><span class="sxs-lookup"><span data-stu-id="cc3df-124">Valid values are: AllUsers and CurrentUser.</span></span> <span data-ttu-id="cc3df-125">Výchozí hodnota je CurrentUser.</span><span class="sxs-lookup"><span data-stu-id="cc3df-125">The default is CurrentUser.</span></span>

<span data-ttu-id="cc3df-126">Určuje obor AllUsers nainstalovat skript do %systemdrive%:\ProgramFiles\WindowsPowerShell\Scripts tak, aby tento skript je k dispozici všem uživatelům.</span><span class="sxs-lookup"><span data-stu-id="cc3df-126">The AllUsers scope specifies to install a script to %systemdrive%:\ProgramFiles\WindowsPowerShell\Scripts so that the script is available to all users.</span></span> <span data-ttu-id="cc3df-127">Oboru CurrentUser Určuje instalaci skript v $home\Documents\WindowsPowerShell\Scripts tak, aby tento skript je k dispozici pouze pro aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="cc3df-127">The CurrentUser scope specifies to install the script in $home\Documents\WindowsPowerShell\Scripts so that the script is available only to the current user.</span></span>


## <a name="nopathupdate"></a><span data-ttu-id="cc3df-128">NoPathUpdate</span><span class="sxs-lookup"><span data-stu-id="cc3df-128">NoPathUpdate</span></span>

- <span data-ttu-id="cc3df-129">NoPathUpdate přepínacího parametru na instalační skript rutiny obchází řádku pro přidání umístění instalovat skriptu do proměnné prostředí PATH.</span><span class="sxs-lookup"><span data-stu-id="cc3df-129">NoPathUpdate switch parameter on Install-Script cmdlet bypasses the prompt for adding the script install location to the PATH environment variable.</span></span>
- <span data-ttu-id="cc3df-130">Jakékoli použití příkazu s – NoPathUpdate zadaný bude mít za následek bez výzvy a zda cesta není aktualizované (vynutit je Ignorovatelná sem).</span><span class="sxs-lookup"><span data-stu-id="cc3df-130">Any use of the command WITH –NoPathUpdate specified will result in no prompt and the PATH NOT being updated (force is ignorable here).</span></span>
- <span data-ttu-id="cc3df-131">-Force bez – NoPathUpdate bude mít za následek bez výzvy a cesta bude aktualizován.</span><span class="sxs-lookup"><span data-stu-id="cc3df-131">-Force without –NoPathUpdate will result in no prompt and the PATH will be updated.</span></span>
- <span data-ttu-id="cc3df-132">Pokud jsou zadané ani – Force, nebo – NoPathUpdate, uživatel uvidí řádku.</span><span class="sxs-lookup"><span data-stu-id="cc3df-132">If neither –Force or –NoPathUpdate are specified, the user will see the prompt.</span></span>
- <span data-ttu-id="cc3df-133">Všechny tyto se vztahuje pouze prvním instalační skript se používá v daném oboru.</span><span class="sxs-lookup"><span data-stu-id="cc3df-133">All of this only applies the first time Install-Script is used in a given scope.</span></span>


## <a name="notes"></a><span data-ttu-id="cc3df-134">Poznámky</span><span class="sxs-lookup"><span data-stu-id="cc3df-134">Notes</span></span>

<span data-ttu-id="cc3df-135">Tato rutina se spustí v prostředí Windows PowerShell 3.0 nebo novější verze prostředí Windows PowerShell na Windows 7 nebo Windows 2008 R2 a pozdějších verzích Windows.</span><span class="sxs-lookup"><span data-stu-id="cc3df-135">This cmdlet runs on Windows PowerShell 3.0 or later releases of Windows PowerShell, on Windows 7 or Windows 2008 R2 and later releases of Windows.</span></span>

<span data-ttu-id="cc3df-136">Pokud hodnota zadaná pro parametr název odpovídá verzi skriptu v počítači a jste nepřidali parametr MinimumVersion nebo RequiredVersion, instalační skript bezobslužné pokračuje bez instalace skriptu.</span><span class="sxs-lookup"><span data-stu-id="cc3df-136">If a version of the script on the computer matches the value specified for the Name parameter, and you have not added the MinimumVersion or RequiredVersion parameter, Install-Script silently continues without installing that script.</span></span> <span data-ttu-id="cc3df-137">Pokud jsou zadány parametry MinimumVersion nebo RequiredVersion a stávající skript neodpovídá hodnoty v tomto parametru, pak dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="cc3df-137">If the MinimumVersion or RequiredVersion parameters are specified, and the existing script does not match the values in that parameter, then an error occurs.</span></span> <span data-ttu-id="cc3df-138">Chcete-li být konkrétnější: Pokud je verze skriptu aktuálně nainstalované nižší než hodnota parametru MinimumVersion nebo není stejná jako hodnota parametru RequiredVersion, dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="cc3df-138">To be more specific: if the version of the currently-installed script is either lower than the value of the MinimumVersion parameter, or not equal to the value of the RequiredVersion parameter, an error occurs.</span></span> <span data-ttu-id="cc3df-139">Pokud je verze nainstalovaného skriptu větší než hodnota parametru MinimumVersion nebo rovna hodnotě parametru RequiredVersion, instalační skript bezobslužné pokračuje bez instalace skriptu.</span><span class="sxs-lookup"><span data-stu-id="cc3df-139">If the version of the installed script is greater than the value of the MinimumVersion parameter, or equal to the value of the RequiredVersion parameter, Install-Script silently continues without installing that script.</span></span>

<span data-ttu-id="cc3df-140">Instalační skript vrátí chybu, pokud žádný skript v galerii online, který odpovídá zadaným názvem neexistuje.</span><span class="sxs-lookup"><span data-stu-id="cc3df-140">Install-Script returns an error if no script exists in the online gallery that matches the specified name.</span></span>

<span data-ttu-id="cc3df-141">Pokud chcete nainstalovat více skriptů, zadejte pole názvů skriptu, oddělených čárkami.</span><span class="sxs-lookup"><span data-stu-id="cc3df-141">To install multiple scripts, specify an array of the script names, separated by commas.</span></span> <span data-ttu-id="cc3df-142">Pokud zadáte více názvů skriptu nelze přidat MinimumVersion nebo RequiredVersion.</span><span class="sxs-lookup"><span data-stu-id="cc3df-142">You cannot add MinimumVersion or RequiredVersion if you specify multiple script names.</span></span>

<span data-ttu-id="cc3df-143">Ve výchozím nastavení skripty jsou nainstalované ke složce Program Files.</span><span class="sxs-lookup"><span data-stu-id="cc3df-143">By default, scripts are installed to the Program Files folder.</span></span> <span data-ttu-id="cc3df-144">Můžete předat více objektů PSGetItemInfo instalační skript; To je další způsob zadávání několik skriptů instalace v jednom příkazu.</span><span class="sxs-lookup"><span data-stu-id="cc3df-144">You can pipe multiple PSGetItemInfo objects to Install-Script; this is another way of specifying multiple scripts to install in a single command.</span></span>

<span data-ttu-id="cc3df-145">Aby se zabránilo spuštěné skripty, které obsahují škodlivý kód, nainstalovat skripty sady nejsou importovány automaticky při instalaci.</span><span class="sxs-lookup"><span data-stu-id="cc3df-145">To help prevent running scripts that contain malicious code, installed scripts are not automatically imported by installation.</span></span> <span data-ttu-id="cc3df-146">Hlediska zabezpečení doporučujeme, před spuštěním jakékoli rutiny nebo funkce ve skriptu pro první vyhodnocení kód skriptu.</span><span class="sxs-lookup"><span data-stu-id="cc3df-146">As a security best practice, evaluate script code before running any cmdlets or functions in a script for the first time.</span></span>


## <a name="cmdlet-syntax"></a><span data-ttu-id="cc3df-147">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="cc3df-147">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Install-Script -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="cc3df-148">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="cc3df-148">Cmdlet online help reference</span></span>

[<span data-ttu-id="cc3df-149">Instalační skript</span><span class="sxs-lookup"><span data-stu-id="cc3df-149">Install-Script</span></span>](http://go.microsoft.com/fwlink/?LinkId=619784)

## <a name="example-commands"></a><span data-ttu-id="cc3df-150">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="cc3df-150">Example commands</span></span>

```powershell


# Piping Find-Script output to Install-Script cmdlet

Find-Script -Repository Local1 -Name Required-Script2

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.5        Required-Script2                    local1               Description for the Required-Script2 script


Find-Script -Repository Local1 -Name Required-Script2 | Install-Script

Get-Command Required-Script2

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
ExternalScript  Required-Script2.ps1                                2.0       C:\Users\manikb\Documents\WindowsPowerShell\Scripts\Required-Script2.ps1


Get-InstalledScript Required-Script2

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.5        Required-Script2                    local1               Description for the Required-Script2 script


Get-InstalledScript Required-Script2 | fl * -Force


Name                       : Required-Script2
Version                    : 2.5
Type                       : Script
Description                : Description for the Required-Script2 script
Author                     : manikb
CompanyName                :
Copyright                  : (c) 2015 Microsoft Corporation. All rights reserved.
PublishedDate              : 8/15/2015 12:42:39 AM
LicenseUri                 : http://required-script2.com/license
ProjectUri                 : http://required-script2.com/
IconUri                    : http://required-script2.com/icon
Tags                       : {Tag1, Tag2, Tag-Required-Script2-2.5, PSScript...}
Includes                   : {Function, DscResource, Cmdlet, Command}
PowerShellGetFormatVersion :
ReleaseNotes               : Required-Script2 release notes
Dependencies               : {}
RepositorySourceLocation   : http://manikb-dev:8765/api/v2/
Repository                 : local1
PackageManagementProvider  : NuGet
InstalledLocation          : C:\Users\manikb\Documents\WindowsPowerShell\Scripts


# Installing a script to AllUsers scope

Install-Script -Repository Local1 -Name Required-Script3 -Scope AllUsers
Get-InstalledScript -Name Required-Script3

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.5        Required-Script3                    local1               Description for the Required-Script3 script


Get-InstalledScript -Name Required-Script3  | fl * -Force


Name                       : Required-Script3
Version                    : 2.5
Type                       : Script
Description                : Description for the Required-Script3 script
Author                     : manikb
CompanyName                :
Copyright                  : (c) 2015 Microsoft Corporation. All rights reserved.
PublishedDate              : 8/15/2015 12:42:45 AM
LicenseUri                 : http://required-script3.com/license
ProjectUri                 : http://required-script3.com/
IconUri                    : http://required-script3.com/icon
Tags                       : {Tag1, Tag2, Tag-Required-Script3-2.5, PSScript...}
Includes                   : {Function, DscResource, Cmdlet, Command}
PowerShellGetFormatVersion :
ReleaseNotes               : Required-Script3 release notes
Dependencies               : {}
RepositorySourceLocation   : http://manikb-dev:8765/api/v2/
Repository                 : local1
PackageManagementProvider  : NuGet
InstalledLocation          : C:\Program Files\WindowsPowerShell\Scripts


# Installing a script with dependent scripts and modules

Find-Script -Repository Local1 -Name Script-WithDependencies2 -IncludeDependencies

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.0        Script-WithDependencies2            local1               Description for the Script-WithDependencies2 script
2.5        RequiredModule1                     local1               RequiredModule1 module
2.5        RequiredModule2                     local1               RequiredModule2 module
2.5        RequiredModule3                     local1               RequiredModule3 module
2.5        Required-Script1                    local1               Description for the Required-Script1 script
2.5        Required-Script2                    local1               Description for the Required-Script2 script
2.5        Required-Script3                    local1               Description for the Required-Script3 script


Install-Script -Repository Local1 -Name Script-WithDependencies2
Get-InstalledScript

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.5        Required-Script1                    local1               Description for the Required-Script1 script
2.5        Required-Script2                    local1               Description for the Required-Script2 script
2.5        Required-Script3                    local1               Description for the Required-Script3 script
2.0        Script-WithDependencies2            local1               Description for the Script-WithDependencies2 script


Get-InstalledModule

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.5        RequiredModule1                     local1               RequiredModule1 module
2.5        RequiredModule2                     local1               RequiredModule2 module
2.5        RequiredModule3                     local1               RequiredModule3 module


Find-Script -Repository Local1 -Name Required-Script*

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.5        Required-Script1                    local1               Description for the Required-Script1 script
2.5        Required-Script2                    local1               Description for the Required-Script2 script
2.5        Required-Script3                    local1               Description for the Required-Script3 script


Install-Script -Repository Local1 -Name Required-Script*

Get-InstalledScript

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.5        Required-Script1                    local1               Description for the Required-Script1 script
2.5        Required-Script2                    local1               Description for the Required-Script2 script
2.5        Required-Script3                    local1               Description for the Required-Script3 script


# Find a script and install it

# The first command finds the script named Required-Script2 from the Local1 repository and displays the results.
# The second command finds the Required-Script2 script, and then uses the pipeline operator to pass it to the Install-Script cmdlet to install it.
# The third command uses the Get-Command cmdlet to get Required-Script2, and then displays the results.
# The fourth command uses the Get-InstalledScript cmdlet to get Required-Script2 and display the results.
# The fifth command gets RequiredScript2 and uses the pipeline operator to pass it to the Format-List cmdlet to format the output.

Find-Script -Repository "Local1" -Name "Required-Script2"

Find-Script -Repository "Local1" -Name "Required-Script2" | Install-Script
Get-Command -Name "Required-Script2"

Get-InstalledScript -Name "Required-Script2"

Get-InstalledScript -Name "Required-Script2" | Format-List * 


# Install a script with AllUsers scope

# The first command installs the script named Required-Script3 and assigns it AllUsers scope.
# The second command gets the installed script Required-Script3 and displays information about it.
# The third command gets Required-Script3 and uses the pipeline operator to pass it to the Format-List cmdlet to format the output.

Install-Script -Repository "Local1" -Name "Required-Script3" -Scope "AllUsers"
Get-InstalledScript -Name "Required-Script3"
Get-InstalledScript -Name "Required-Script3" | Format-List * 


# Install a script with its dependent scripts and modules

# The first command finds the script named Script-WithDependencies2 and its dependencies in the Local1 repository and displays the results.
# The second command installs Script-WithDependencies2.
# The third command uses the Get-InstalledScript script cmdlet to get installed scripts and display the results.
# The fourth command uses the Get-InstalledModule cmdlet to get installed modules and display the results.
# The fifth command uses the Find-Script cmdlet to find scripts where the name begins with Required-Script and display the results.
# The sixth command installs the scripts where the name begins with Required-Script in the Local1 repository. 
# The final command gets installed scripts and displays the results.

Find-Script -Repository "Local1" -Name "Script-WithDependencies2" -IncludeDependencies
Install-Script -Repository "Local1" -Name "Script-WithDependencies2"
Get-InstalledScript
Get-InstalledModule
Find-Script -Repository "Local1" -Name "Required-Script*"
Install-Script -Repository "Local1" -Name "Required-Script*"
Get-InstalledScript

```

<span data-ttu-id="cc3df-151">Můžete taky Get-Command – název <InstalledScriptFileName> ho.</span><span class="sxs-lookup"><span data-stu-id="cc3df-151">You can also use Get-Command –Name <InstalledScriptFileName> to get it.</span></span> <span data-ttu-id="cc3df-152">Umístění instalace dvou se přidají do proměnné prostředí PATH na první použití zadaného oboru.</span><span class="sxs-lookup"><span data-stu-id="cc3df-152">Two install locations are added to the PATH environment variable on first use of a specified scope.</span></span>
```powershell
$env:Path -split ';'| Where-Object {$\_} | Select-Object -Last 2
C:\\Program Files\\WindowsPowerShell\\Scripts
C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Scripts

Get-Command Required-Script2
CommandType Name Version Source
----------- ---- ------- ------
ExternalScript Required-Script2.ps1 C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Scripts\\Required-Script2.ps1
```

```powershell

# Install a script by name
Install-Script -Name MyDscscript

# Install multiple scripts
Install-Script ContosoClient,ContosoServer

# Install a script using its minimum version
Install-Script -Name ContosoServer -MinimumVersion 1.0

# Install a specific version of a script
Install-Script -Name ContosoServer -RequiredVersion 1.1.3

# Install a specific prerelease version of a script
Install-Script -Name ContosoServer -RequiredVersion 1.1.3-alpha -AllowPrerelease

# Install the latest version of a script to $home\Documents\WindowsPowerShell\scripts.
Install-Script -Name ContosoServer -Scope CurrentUser

# if a script is already available under $env:PSModulePath, below command fails with 'scriptAlreadyInstalled,Install-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage'
Install-Script ContosoServer -RequiredVersion 1.5

# if a script is already available under $env:PSModulePath, below command fails with 'scriptAlreadyInstalled,Install-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage'
Install-Script ContosoServer -MinimumVersion 2.5

# Install multiple scripts from multiple registered repositories
Install-Script ContosoClient,ContosoServer -Repository PSGallery, PrivatePSGallery

# Install a script with -WhatIf
Install-Script ContosoClient -WhatIf

# Install a script with -Confirm. A prompt will be displayed to confirm the installation.
Install-Script ContosoClient -WhatIf

# -Force option reinstalls the installed script
Install-Script ContosoClient -Force

# Install a script with dependencies
Install-Script -Name ContosoClient

# Install a script 

# Install a script from the registered repository with ScriptSourceLocation
Install-Script Connect-AzureVM

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0        Connect-AzureVM                     PSGallery            This runbook sets up a connection to an Azure vi...

# Find multiple scripts
Install-Script -Name Connect-AzureVM, Show-Tree, Connect-O365

# Find scripts with wildcards in -Name
Install-Script -Name *Azure*

# Find all versions of a script
Install-Script -Name Connect-O365 -AllVersions

# Find a script with -MinimumVersion. 
# With MinimumVersion we can find a script whose version is greate than or equal to the specified MinimumVersion value.
Install-Script Connect-O365 -MinimumVersion 1.4

# Find a script with MaximumVersion
Install-Script -Name Connect-O365 -MaximumVersion 1.6.2

# Find a script with both MinimumVersion and MaximumVersion range.
Install-Script -Name Connect-O365 -MinimumVersion 1.1 -MaximumVersion 1.6.2

# Installing a script to default AllUsers scope and with RequiredVersion
Install-Script -Name Connect-O365 -RequiredVersion 1.5.7

# Find a script from the specified repository
Install-Script -Name Fabrikam-ServerScript -Repository MyLocalRepo

# Find available scripts from all registered repositories
Install-Script

# Find available scripts from few registered repositories
Install-Script -Repository PSGallery, PrivatePSGallery

```

```powershell
 Added the logic for checking and failing the install script operation when there is a command with same name is already available on the system.
Also updated the prompt message.

 Examples:
PS C:\WINDOWS\system32> install-script get-childitem -Repository localrepo
install-script : A command with name 'get-childitem' is already available on this system. This script 'get-childitem' may override the existing command. If you still want to install this script 'get-childitem', use -Force parameter.
At line:1 char:1
+ install-script get-childitem -Repository localrepo
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
     + CategoryInfo          : InvalidOperation: (:) [Write-Error], WriteErrorException
     + FullyQualifiedErrorId : CommandAlreadyAvailableWitScriptName,Install-Script

 
 
 PS C:\WINDOWS\system32> install-script get-childitem,contosos -Repository localrepo
install-script : A command with name 'get-childitem' is already available on this system. This script 'get-childitem' may override the existing command. If you still want to install this script 'get-childitem', use -Force parameter.
At line:1 char:1
+ install-script get-childitem,contosos -Repository localrepo
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
     + CategoryInfo          : InvalidOperation: (:) [Write-Error], WriteErrorException
     + FullyQualifiedErrorId : CommandAlreadyAvailableWitScriptName,Install-Script

 PackageManagement\Install-Package : No match was found for the specified search criteria and script name 'contosos'. Try Get-ScriptRepository to see all available registered script repositories.
At C:\Program Files\WindowsPowerShell\Modules\powershellget\1.0.0.1\PSModule.psm1:2891 char:21
+ ...          $null = PackageManagement\Install-Package @PSBoundParameters
+                      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
     + CategoryInfo          : ObjectNotFound: (Microsoft.Power....InstallPackage:InstallPackage) [Install-Package], Exception
     + FullyQualifiedErrorId : NoMatchFoundForCriteria,Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage

 PS C:\WINDOWS\system32>

 
 
 PS C:\WINDOWS\system32> find-script get-childitem -Repository localrepo | install-script
install-script : A command with name 'get-childitem' is already available on this system. This script 'get-childitem' may override the existing command. If you still want to install this script 'get-childitem', use -Force parameter.
At line:1 char:51
+ find-script get-childitem -Repository localrepo | install-script
+                                                   ~~~~~~~~~~~~~~
     + CategoryInfo          : InvalidOperation: (:) [Write-Error], WriteErrorException
     + FullyQualifiedErrorId : CommandAlreadyAvailableWitScriptName,Install-Script

 
 PS C:\WINDOWS\system32>

 PS C:\WINDOWS\system32> Install-Package -Name Get-ChildItem -source LocalRepo  -ProviderName powershellget -Type Script
WARNING: A command with name 'get-childitem' is already available on this system. This script 'get-childitem' may override the existing command. If you still want to install this script 'get-childitem', use -Force parameter.

```

```powershell

Prompt ONCE per USER and per SCOPE for adding the script installation location to PATH environment variable.

- Prompt message for CurrentUser scope: (Complete message will be scrubbed later)

Acceptance required for adding the script installation locations to the PATH environment variable
The scripts install location 'C:\Users\manikb\Documents\WindowsPowerShell\Scripts' is required to be added to the PATH environment variable in order to execute an installed script with only file name along with its script dependencies. If you accept this prompt, 'C:\Users\manikb\Documents\WindowsPowerShell\Scripts' will be added to system specific PATH environment variable and process specific $env:PATH variable, if not already added. Otherwise you will have to use the full file path to  execute an installed script. Alternatively, you can use Save-Script cmdlet to download the script files to your favorite location. This prompt can be avoided and automatically considered as opted-out by adding 'C:\Users\manikb\Documents\WindowsPowerShell\Scripts' install location to the PATH environment variable or to the $env:PATH variable of current process. Do you want to continue?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):


- Prompt message for –AllUsers scope is same as above with $env:ProgramFiles\WindowsPowerShell\Scripts .

Acceptance required for adding the script installation locations to the PATH environment variable
The scripts install location 'C:\Program Files\WindowsPowerShell\Scripts' is required to be added to the PATH environment variable in order to execute an installed script with only file name along with its script dependencies. If you accept this prompt, 'C:\Program Files\WindowsPowerShell\Scripts' will be added to system specific PATH environment variable and process specific $env:PATH variable, if not already added. Otherwise you will have to use the full file path to  execute an installed script. Alternatively, you can use Save-Script cmdlet to download the script files to your favorite location. This prompt can be avoided and automatically considered as opted-out by adding 'C:\Program Files\WindowsPowerShell\Scripts' install location to the PATH environment variable or to the $env:PATH variable of current process. Do you want to continue?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):


- To prompt only once per scope, user acceptance for PATH variable change will be added to the user specific settings file under %localappdata%\Microsoft\windows\PowerShell\PowerShellGet
%localappdata%\Microsoft\windows\PowerShell\PowerShellGet\PowerShellGetSettings.XML. 
This settings file will be used to not prompt again.

After prompting for CurrentUser scope: 
    true or false for CurrentUserScope_AllowPATHChangeForScripts key based on user input.

After prompting for AllUsers scope: 
    true or false for AllUsersScope_AllowPATHChangeForScripts key based on user input.

- If user accepts the prompt
                Check and add $home\Documents\WindowsPowerShell\Scripts to user specific PATH environment variable.
                Check and add $env:ProgramFiles\WindowsPowerShell\Scripts to system specific PATH environment variable only when Install-Script cmdlet is used in an administrator process.
                Check and add above two paths to $env:PATH variable of the current process.

- If user denies the prompt, script installation will be proceeded without making any changes to the PATH environment variable.



Example:             
PS C:\windows\system32> Install-Script -Name $scriptName -Repository $repositoryName -Scope $Scope -Verbose

Acceptance required for adding the script installation locations to the PATH environment variable
The scripts install location 'C:\Program Files\WindowsPowerShell\Scripts' is required to be added to the PATH environment variable in order to execute an installed script with only file name along with its script dependencies. If you accept this prompt, 'C:\Program Files\WindowsPowerShell\Scripts' will be added to system specific PATH environment variable and process specific $env:PATH variable, if not already added. Otherwise you will have to use the full file path to  execute an installed script. Alternatively, you can use Save-Script cmdlet to download the script files to your favorite location. This prompt can be avoided and automatically considered as opted-out by adding 'C:\Program Files\WindowsPowerShell\Scripts' install location to the PATH environment variable or to the $env:PATH variable of current process. Do you want to continue?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): n


```

## <a name="install-script-cmdlet-in-pipeline-operations"></a><span data-ttu-id="cc3df-153">Instalační skript rutiny v operacích kanálu</span><span class="sxs-lookup"><span data-stu-id="cc3df-153">Install-Script cmdlet in pipeline operations</span></span>

```powershell

# Find a script and install it
Find-Script -Name "MyDSC*" | Install-Script

# Find a script and install it to the CurrentUser scope
Find-Script -Name "MyDSC*" | Install-Script -Scope CurrentUser

# Find commands by name and install them
# The first command finds the specified commands in the INT repository, and then uses the pipeline operator to pass them to Install-Script to install them.
# The second command uses Get-Installedscript to verify the scripts from the prior command are installed.
Find-Command -Repository "INT" -Name Get-ContosoClient,Get-ContosoServer | Install-Script
Get-Installedscript

# Find multiple role capabilities and install them
Find-RoleCapability -Name MyJeaRole, Maintenance | Install-Script
Get-Installedscript

```



## <a name="error-scenarios"></a><span data-ttu-id="cc3df-154">Chyba scénáře</span><span class="sxs-lookup"><span data-stu-id="cc3df-154">Error scenarios</span></span>

```powershell

# Below command fails with 'NameShouldNotContainWildcardCharacters,Install-Script'
Install-Script ContosoServe*

# Below command fails with 'VersionRangeAndRequiredVersionCannotBeSpecifiedTogether,Install-Script'
Install-Script ContosoServer -MinimumVersion 1.0 -RequiredVersion 5.0

# Below command fails with 'VersionParametersAreAllowedOnlyWithSingleName,Install-Script'
Install-Script ContosoClient,ContosoServer -RequiredVersion 2.0

# Below command fails with 'VersionParametersAreAllowedOnlyWithSingleName,Install-Script'
Install-Script ContosoClient,ContosoServer -MinimumVersion 2.0

```

## <a name="install-script-and-get-installedscript-cmdlets"></a><span data-ttu-id="cc3df-155">Instalační skript a Get-InstalledScript rutiny</span><span class="sxs-lookup"><span data-stu-id="cc3df-155">Install-Script and Get-InstalledScript cmdlets</span></span>
<span data-ttu-id="cc3df-156">Instalační skript rutiny umožňuje instalaci souboru specifického skriptu společně s jeho závislosti na zadaném oboru.</span><span class="sxs-lookup"><span data-stu-id="cc3df-156">Install-Script cmdlet lets you to install a specific script file along with its dependencies to the specified scope.</span></span> <span data-ttu-id="cc3df-157">Ve výchozím nastavení skripty jsou nainstalované na AllUsers obor.</span><span class="sxs-lookup"><span data-stu-id="cc3df-157">By default, scripts are installed to the AllUsers scope.</span></span> <span data-ttu-id="cc3df-158">Rutina Get-InstalledScript umožňuje načíst seznam souborů skriptů, které jsou nainstalované s použitím rutiny instalační skript.</span><span class="sxs-lookup"><span data-stu-id="cc3df-158">Get-InstalledScript cmdlet lets you to get the list of script files which were installed using Install-Script cmdlet.</span></span>

<span data-ttu-id="cc3df-159">Použití Poznámka: umožňující správu a vyhledání skripty po jejich instalaci instalační skript se vytvořit výchozí složku pro ukládání skriptů v $home\Documents\WindowsPowerShell\Scripts a přidejte této složky pro vaše prostředí cesta.</span><span class="sxs-lookup"><span data-stu-id="cc3df-159">Use note: To allow management and locating of scripts once they are installed, Install-script will create a default folder for storing scripts at $home\Documents\WindowsPowerShell\Scripts, and add that folder to your PATH environment.</span></span> <span data-ttu-id="cc3df-160">Pokud úprava cesta je důležité, použijte skript uložit místo instalační skript.</span><span class="sxs-lookup"><span data-stu-id="cc3df-160">If modifying the path is a concern, use Save-Script instead of Install-Script.</span></span> <span data-ttu-id="cc3df-161">Get-InstalledScripts a odinstalační skript můžete pracovat pouze s skripty, které jsou umístěny v systému pomocí instalační skript.</span><span class="sxs-lookup"><span data-stu-id="cc3df-161">Get-InstalledScripts and Uninstall-Script can only work with scripts placed on the system using Install-Script.</span></span>
```powershell
# Install locations for scripts:
# Default scope is AllUsers.
# AllUsers scope --> "$env:ProgramFiles\\WindowsPowerShell\\Scripts"
# CurrentUser scope -->; "$env:USERPROFILE\\Documents\\WindowsPowerShell\\Scripts"

# Piping Find-Script output to Install-Script cmdlet
Find-Script -Repository GalleryINT -Name Required-Script2 | Install-Script -Scope CurrentUser -Verbose
VERBOSE: Repository details, Name = 'GalleryINT', Location = 'https://customgallery.cloudapp.net/api/v2/'; IsTrusted = 'True'; IsRegistered = 'True'.
VERBOSE: Performing the operation "Install-Script" on target "Version '2.5' of script 'Required-Script2'".
VERBOSE: Using the provider 'PowerShellGet' for searching packages.
VERBOSE: Using the specified source names : 'GalleryINT'.
VERBOSE: Getting the provider object for the PackageManagement Provider 'NuGet'.
VERBOSE: The specified Location is 'https://customgallery.cloudapp.net/api/v2/items/psscript/' and PackageManagementProvider is 'NuGet'.
VERBOSE: Searching repository 'https://customgallery.cloudapp.net/api/v2/items/psscript/FindPackagesById()?id='Required-Script2'' for ''.
VERBOSE: Total package yield:'1' for the specified package 'Required-Script2'.
VERBOSE: Performing the operation "Install-Script" on target "Version '2.5' of script 'Required-Script2'".
VERBOSE: The installation scope is specified to be 'CurrentUser'.
VERBOSE: The specified script will be installed in 'C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Scripts' and its dependent modules will be installed in
'C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Modules'.
VERBOSE: The specified Location is 'NuGet' and PackageManagementProvider is 'NuGet'.
VERBOSE: Downloading script 'Required-Script2' with version '2.5' from the repository 'https://customgallery.cloudapp.net/api/v2/items/psscript/'.
VERBOSE: Script 'Required-Script2' was installed successfully.

Get-InstalledScript Required-Scri\*
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script

Get-InstalledScript Required-Script2 | Format-List \* -Force
Name : Required-Script2
Version : 2.5
Type : Script
Description : Description for the Required-Script2 script
Author : manikb
CompanyName :
Copyright : (c) 2015 Microsoft Corporation. All rights reserved.
PublishedDate : 10/30/2015 1:25:15 AM
LicenseUri : http://required-script2.com/license
ProjectUri : http://required-script2.com/
IconUri : http://required-script2.com/icon
Tags : {Tag1, Tag2, Tag-Required-Script2-2.5, PSScript}
Includes : {Function, DscResource, Cmdlet, Workflow...}
PowerShellGetFormatVersion :
ReleaseNotes : Required-Script2 release notes
Dependencies : {}
RepositorySourceLocation : https://customgallery.cloudapp.net/api/v2/
Repository : GalleryINT
PackageManagementProvider : NuGet
AdditionalMetadata : {Type, releaseNotes, copyright, PackageManagementProvider...}
InstalledLocation : C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Scripts

Installed script file is immediately available for usage.
```

<span data-ttu-id="cc3df-162">Můžete taky Get-Command – název <InstalledScriptFileName> ho.</span><span class="sxs-lookup"><span data-stu-id="cc3df-162">You can also use Get-Command –Name <InstalledScriptFileName> to get it.</span></span> <span data-ttu-id="cc3df-163">Umístění instalace dvou se přidají do proměnné prostředí PATH na první použití zadaného oboru.</span><span class="sxs-lookup"><span data-stu-id="cc3df-163">Two install locations are added to the PATH environment variable on first use of a specified scope.</span></span>
```powershell
$env:Path -split ';'| Where-Object {$\_} | Select-Object -Last 2
C:\\Program Files\\WindowsPowerShell\\Scripts
C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Scripts

Get-Command Required-Script2
CommandType Name Version Source
----------- ---- ------- ------
ExternalScript Required-Script2.ps1 C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Scripts\\Required-Script2.ps1

Find-Script -Repository LocalRepo1 -Name Demo-Script
Version Name Type Repository Description
------- ---- ---- ---------- -----------
1.0 Demo-Script Script LocalRepo1 Script file description goes here

Find-Script -Repository LocalRepo1 -Name Demo-Script | Install-Script -Scope CurrentUser
Untrusted repository
You are installing the scripts from an untrusted repository. If you trust this repository, change its InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the scripts from 'C:\\MyLocalRepo'?
[Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "N"): Y

Get-InstalledScript Demo-Script
Version Name Type Repository Description
------- ---- ---- ---------- -----------
1.0 Demo-Script Script LocalRepo1 Script file description goes here

Get-Command Demo-Script
CommandType Name Version Source
----------- ---- ------- ------
ExternalScript Demo-Script.ps1 C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Scripts\\Demo-Script.ps1

# Using the installed script
Demo-Script
Demo-ScriptFunction
Demo-ScriptWorkflow

# Installing a script to default AllUsers scope and with RequiredVersion
Install-Script -Repository GalleryINT -Name Required-Script3 -RequiredVersion 2.0
Get-InstalledScript -Name Required-Script3

Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.0 Required-Script3 Script GalleryINT Description for the Required-Script3 script
Get-InstalledScript -Name Required-Script3 | Format-List Name,InstalledLocation -Force
Name : Required-Script3
InstalledLocation : C:\\Program Files\\WindowsPowerShell\\Scripts

Get-Command Required-Script3
CommandType Name Version Source
----------- ---- ------- ------
ExternalScript Required-Script3.ps1 C:\\Program Files\\WindowsPowerShell\\Scripts\\Required-Script3.ps1

# Installing a script with dependent scripts and modules
Find-Script -Repository GalleryINT -Name Script-WithDependencies2 -IncludeDependencies
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.0 Script-WithDependencies2 Script GalleryINT Description for the Script-WithDependencies2 script
2.5 RequiredModule1 Module GalleryINT RequiredModule1 module
2.5 RequiredModule2 Module GalleryINT RequiredModule2 module
2.5 RequiredModule3 Module GalleryINT RequiredModule3 module
2.0 RequiredModule4 Module GalleryINT RequiredModule4 module
1.5 RequiredModule5 Module GalleryINT RequiredModule5 module
2.5 Required-Script1 Script GalleryINT Description for the Required-Script1 script
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script
2.5 Required-Script3 Script GalleryINT Description for the Required-Script3 script

Get-InstalledScript
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.0 Required-Script3 Script GalleryINT Description for the Required-Script3 script
1.0 Demo-Script Script LocalRepo1 Script file description goes here
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script
Get-InstalledModule
Install-Script -Repository GalleryINT -Name Script-WithDependencies2 -Scope CurrentUser
Get-InstalledScript
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.0 Required-Script3 Script GalleryINT Description for the Required-Script3 script
1.0 Demo-Script Script LocalRepo1 Script file description goes here
2.5 Required-Script1 Script GalleryINT Description for the Required-Script1 script
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script
2.0 Script-WithDependencies2 Script GalleryINT Description for the Script-WithDependencies2 script
Get-InstalledModule
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.5 RequiredModule1 Module GalleryINT RequiredModule1 module
2.5 RequiredModule2 Module GalleryINT RequiredModule2 module
2.5 RequiredModule3 Module GalleryINT RequiredModule3 module
2.0 RequiredModule4 Module GalleryINT RequiredModule4 module
1.5 RequiredModule5 Module GalleryINT RequiredModule5 module

# Contents of Script-WithDependencies2 file.
<#PSScriptInfo
.VERSION 2.0
.GUID 90082fa1-0b84-49fb-a00e-0a624fbb6584
.AUTHOR manikb
.COMPANYNAME Microsoft Corporation
.COPYRIGHT (c) 2015 Microsoft Corporation. All rights reserved.
.TAGS Tag1 Tag2 Tag-Script-WithDependencies2-2.0
.LICENSEURI http://script-withdependencies2.com/license
.PROJECTURI http://script-withdependencies2.com/
.ICONURI http://script-withdependencies2.com/icon
.EXTERNALMODULEDEPENDENCIES
.REQUIREDSCRIPTS Required-Script1,Required-Script2,Required-Script3
.EXTERNALSCRIPTDEPENDENCIES
.RELEASENOTES
Script-WithDependencies2 release notes
#>
#Requires -Module RequiredModule1
#Requires -Module @{ModuleName = 'RequiredModule2'; ModuleVersion = '2.0'}
#Requires -Module @{RequiredVersion = '2.5'; ModuleName = 'RequiredModule3'}
#Requires -Module @{ModuleVersion = '1.1'; ModuleName = 'RequiredModule4'; MaximumVersion = '2.0'}
#Requires -Module @{MaximumVersion = '1.5'; ModuleName = 'RequiredModule5'}
<#
.DESCRIPTION
Description for the Script-WithDependencies2 script
#>
Param()
Function Test-FunctionFromScript\_Script-WithDependencies2 { Get-Date }
Workflow Test-WorkflowFromScript\_Script-WithDependencies2 { Get-Date }
```

