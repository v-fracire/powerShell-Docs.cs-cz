---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: Instalace modulu
ms.openlocfilehash: c066f4b34a03206cc0f31e9d40144fd719d9e305
ms.sourcegitcommit: 58371abe9db4b9a0e4e1eb82d39a9f9e187355f9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/05/2017
---
# <a name="install-module"></a>Instalace modulu

Nainstaluje na moduly Powershellu z online úložiště na místním počítači.

## <a name="description"></a>Popis

Rutiny Install-Module stáhne jeden nebo více modulů z online galerie, ověří a nainstaluje je do oboru zadanou instalaci místního počítače.

Rutina Install-Module získá jeden nebo více modulů, které splňují zadaná kritéria z online galerie, ověří, že výsledky hledání jsou platné moduly a kopie modulu složek do umístění instalace.

Pokud je definován žádný obor, nebo pokud je hodnota parametru oboru AllUsers, je modul nainstalován na %systemdrive%:\Program Files\WindowsPowerShell\Modules. Pokud je hodnota oboru CurrentUser, modul nainstalován na $home\Documents\WindowsPowerShell\Modules.

Můžete filtrovat výsledky podle minimální a přesné verze zadané moduly.

- Podpora verzí vedle sebe na prostředí Windows PowerShell 5.0 nebo novější
- Podpora instalace závislostí modulu
- **Nedůvěryhodná zeptat:**přijetí uživateli je požadováno pro instalaci modulů z nedůvěryhodné úložiště.
- -Force přeinstaluje nainstalovaný modul
- RequiredVersion nainstaluje zadaná verze v SxS s existující verze na rozhraní PowerShell verze 5.0 nebo novější.

### <a name="scope"></a>Obor
Určuje obor instalace modulu. Přípustné hodnoty tohoto parametru jsou: AllUsers a CurrentUser.

Výchozí instalace obor je AllUsers.

Oboru AllUsers umožňuje moduly nainstalovat do umístění, které je přístupné pro všechny uživatele počítače, který je "$env: SystemDrive\Program Files\WindowsPowerShell\Modules".

Oboru CurrentUser umožňuje moduly nainstalována pouze pro "$home\Documents\WindowsPowerShell\Modules", tak, aby modulu je k dispozici pouze pro aktuálního uživatele.

## <a name="notes"></a>Poznámky

Tato rutina se spustí v prostředí Windows PowerShell 3.0 nebo novější verze prostředí Windows PowerShell na Windows 7 nebo Windows 2008 R2 a pozdějších verzích Windows.

Pokud nainstalovaný modul nelze importovat (to znamená, pokud nemá .psm1, .psd1 nebo .dll se stejným názvem ve složce), instalace se nezdaří, pokud do příkazu přidáte parametr Force.

Pokud hodnota zadaná pro parametr název odpovídá verzi modulu v počítači a jste nepřidali parametr MinimumVersion nebo RequiredVersion, instalace modulu bezobslužně pokračuje bez instalace tohoto modulu. Pokud jsou zadány parametry MinimumVersion nebo RequiredVersion a existující modul neodpovídá hodnoty v tomto parametru, pak dojde k chybě. Chcete-li být konkrétnější: Pokud je verze modulu aktuálně nainstalované nižší než hodnota parametru MinimumVersion nebo není stejná jako hodnota parametru RequiredVersion, dojde k chybě. Pokud verze nainstalovaný modul je větší než hodnota parametru MinimumVersion nebo rovna hodnotě parametru RequiredVersion, bude pokračovat bezobslužná instalace modulu bez instalace tohoto modulu.

Instalace modulu vrátí chybu, pokud žádný modul v galerii online, který odpovídá zadaným názvem neexistuje.

Pokud chcete nainstalovat více modulů, zadejte pole názvy modulů, oddělených čárkami. Pokud zadáte více názvů modulu nelze přidat MinimumVersion nebo RequiredVersion.

Ve výchozím nastavení jsou ke složce Program Files, aby nedošlo k záměně při instalaci požadovaného stavu aplikace Windows PowerShell (DSC) prostředky nainstalované moduly. Můžete předat více objektů PSGetItemInfo k instalaci modulu; To je další způsob zadávání více modulů k instalaci v jednom příkazu.

To pomáhá zabránit spuštěných modulů, které obsahují škodlivý kód, nainstalované moduly sady nejsou importovány automaticky při instalaci. Hlediska zabezpečení doporučujeme, před spuštěním jakékoli rutiny nebo funkce v modulu první vyhodnocení modulu kódu.


## <a name="cmdlet-syntax"></a>Syntaxe rutin
```powershell
Get-Command -Name Install-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>Referenční informace o rutinách online nápovědy

[Instalace modulu](http://go.microsoft.com/fwlink/?LinkID=398573)

## <a name="example-commands"></a>Příklady příkazů

```powershell

# Install a module by name
Install-Module -Name MyDscModule

# Install multiple modules
Install-Module ContosoClient,ContosoServer

# Install a module using its minimum version
Install-Module -Name ContosoServer -MinimumVersion 1.0

# Install a specific version of a module
Install-Module -Name ContosoServer -RequiredVersion 1.1.3

# Install a specific prerelease version of a module
Install-Module -Name ContosoServer -RequiredVersion 1.1.3-alpha -AllowPrerelease

# Install the latest version of a module by name, including prelrelease versions if one exists
Install-Module -Name ContosoServer -AllowPrerelease

# Install the latest version of a module to $home\Documents\WindowsPowerShell\Modules.
Install-Module -Name ContosoServer -Scope CurrentUser

# if a module is already available under $env:PSModulePath, below command fails with 'ModuleAlreadyInstalled,Install-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage'
Install-Module ContosoServer -RequiredVersion 1.5

# if a module is already available under $env:PSModulePath, below command fails with 'ModuleAlreadyInstalled,Install-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage'
Install-Module ContosoServer -MinimumVersion 2.5

# Install multiple modules from multiple registered repositories
Install-Module ContosoClient,ContosoServer -Repository PSGallery, PrivatePSGallery

# Install a module with -WhatIf
Install-Module ContosoClient -WhatIf

# Install a module with -Confirm. A prompt will be displayed to confirm the installation.
Install-Module ContosoClient -WhatIf

# -Force option reinstalls the installed module
Install-Module ContosoClient -Force

# Install a module with dependencies
Install-Module -Name 
```

## <a name="install-module-cmdlet-in-pipeline-operations"></a>Instalace modulu rutiny v operacích kanálu

```powershell

# Find a module and install it
Find-Module -Name "MyDSC*" | Install-Module

# Find a module and install it to the CurrentUser scope
Find-Module -Name "MyDSC*" | Install-Module -Scope CurrentUser

# Find commands by name and install them
# The first command finds the specified commands in the INT repository, and then uses the pipeline operator to pass them to Install-Module to install them.
# The second command uses Get-InstalledModule to verify the modules from the prior command are installed.
Find-Command -Repository "INT" -Name Get-ContosoClient,Get-ContosoServer | Install-Module
Get-InstalledModule

# This command finds the resource named MyResource and passes it to the Install-Module cmdlet by using the pipeline operator. The Install-Module cmdlet installs the module for the resource. 
# If you pipe multiple resources to the Install-Module cmdlet from the same module, Install-Module attempts to install the module only once. 
Find-DscResource -Name "MyResource" | Install-Module
Get-InstalledModule

# Find multiple role capabilities and install them
Find-RoleCapability -Name MyJeaRole, Maintenance | Install-Module
Get-InstalledModule

```

## <a name="side-by-side-version-support-on-powershell-50-or-newer"></a>Podpora verzí vedle sebe na prostředí PowerShell 5.0 nebo novější

PowerShellGet podporuje verze podpora vedle sebe (SxS) modulu v instalaci modulu, aktualizace modulu a publikovat modul rutin, které spustit v prostředí Windows PowerShell 5.0 nebo novější.

### <a name="install-module-examples"></a>Instalace modulu příklady

```powershell
# Install a version of the module
Install-Module -Name PSScriptAnalyzer -RequiredVersion 1.1.0 -Repository PSGallery
Get-Module -ListAvailable -Name PSScriptAnalyzer | Format-List Name,Version,ModuleBase

Name : PSScriptAnalyzer
Version : 1.1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.0

# Install another version of the module in Side-by-Side with already installed version.
Install-Module -Name PSScriptAnalyzer -RequiredVersion 1.1.1 -Repository PSGallery
Get-Module -ListAvailable -Name PSScriptAnalyzer | Format-List Name,Version,ModuleBase

Name       : PSScriptAnalyzer 
Version    : 1.1.1
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.1
Name       : PSScriptAnalyzer
Version    : 1.1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.0

# Get all versions of an installed module
Get-InstalledModule -Name PSScriptAnalyzer -AllVersions
Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.1.0      PSScriptAnalyzer                    PSGallery            PSScriptAnalyzer provides script analysis... 
1.1.1      PSScriptAnalyzer                    PSGallery            PSScriptAnalyzer provides script analysis...


```

## <a name="install-module-with-its-dependencies"></a>Instalace modulu s jeho závislé součásti

```powershell

# Find a module
Find-Module -Name TypePx -Repository PSGallery

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.0.1.20   TypePx                              PSGallery            The TypePx module adds properties and methods to the m...

# Find a module and its dependencies
Find-Module -Name TypePx -Repository PSGallery -IncludeDependencies

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.0.1.20   TypePx                              PSGallery            The TypePx module adds properties and methods to the m...
1.0.5.18   SnippetPx                           PSGallery            The SnippetPx module enhances the snippet experience i...

# Discover the dependencies list without adding -IncludeDependencies
$result = Find-Module -Name TypePx -Repository PSGallery
$result.Dependencies

Name                           Value
----                           -----
Name                           SnippetPx
CanonicalId                    powershellget:SnippetPx/#https://www.powershellgallery.com/api/v2/


# Now install the module along with its dependencies
Install-Module -Name TypePx -Repository PSGallery -Verbose

VERBOSE: Repository details, Name = 'PSGallery', Location = 'https://www.powershellgallery.com/api/v2/'; IsTrusted =
'False'; IsRegistered = 'True'.
VERBOSE: Using the provider 'PowerShellGet' for searching packages.
VERBOSE: Using the specified source names : 'PSGallery'.
VERBOSE: Getting the provider object for the PackageManagement Provider 'NuGet'.
VERBOSE: The specified Location is 'https://www.powershellgallery.com/api/v2/' and PackageManagementProvider is
'NuGet'.
VERBOSE: Searching repository 'https://www.powershellgallery.com/api/v2/FindPackagesById()?id='TypePx'' for ''.
VERBOSE: Total package yield:'1' for the specified package 'TypePx'.
VERBOSE: Performing the operation "Install-Module" on target "Version '2.0.1.20' of module 'TypePx'".

Untrusted repository
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Y
VERBOSE: The installation scope is specified to be 'AllUsers'.
VERBOSE: The specified module will be installed in 'C:\Program Files\WindowsPowerShell\Modules'.
VERBOSE: The specified Location is 'NuGet' and PackageManagementProvider is 'NuGet'.
VERBOSE: Downloading module 'TypePx' with version '2.0.1.20' from the repository
'https://www.powershellgallery.com/api/v2/'.
VERBOSE: Searching repository 'https://www.powershellgallery.com/api/v2/FindPackagesById()?id='TypePx'' for ''.
VERBOSE: Searching repository 'https://www.powershellgallery.com/api/v2/FindPackagesById()?id='SnippetPx'' for ''.
VERBOSE: InstallPackage' - name='SnippetPx',
version='1.0.5.18',destination='C:\Users\manikb\AppData\Local\Temp\1027042896'
VERBOSE: DownloadPackage' - name='SnippetPx',
version='1.0.5.18',destination='C:\Users\manikb\AppData\Local\Temp\1027042896\SnippetPx\SnippetPx.nupkg',
uri='https://www.powershellgallery.com/api/v2/package/SnippetPx/1.0.5.18'
VERBOSE: Downloading 'https://www.powershellgallery.com/api/v2/package/SnippetPx/1.0.5.18'.
VERBOSE: Completed downloading 'https://www.powershellgallery.com/api/v2/package/SnippetPx/1.0.5.18'.
VERBOSE: Completed downloading 'SnippetPx'.
VERBOSE: Hash for package 'SnippetPx' does not match hash provided from the server.
VERBOSE: InstallPackageLocal' - name='SnippetPx',
version='1.0.5.18',destination='C:\Users\manikb\AppData\Local\Temp\1027042896'
VERBOSE: InstallPackage' - name='TypePx',
version='2.0.1.20',destination='C:\Users\manikb\AppData\Local\Temp\1027042896'
VERBOSE: DownloadPackage' - name='TypePx',
version='2.0.1.20',destination='C:\Users\manikb\AppData\Local\Temp\1027042896\TypePx\TypePx.nupkg',
uri='https://www.powershellgallery.com/api/v2/package/TypePx/2.0.1.20'
VERBOSE: Downloading 'https://www.powershellgallery.com/api/v2/package/TypePx/2.0.1.20'.
VERBOSE: Completed downloading 'https://www.powershellgallery.com/api/v2/package/TypePx/2.0.1.20'.
VERBOSE: Completed downloading 'TypePx'.
VERBOSE: Hash for package 'TypePx' does not match hash provided from the server.
VERBOSE: InstallPackageLocal' - name='TypePx',
version='2.0.1.20',destination='C:\Users\manikb\AppData\Local\Temp\1027042896'
VERBOSE: Installing the dependency module 'SnippetPx' with version '1.0.5.18' for the module 'TypePx'.
VERBOSE: Module 'SnippetPx' was installed successfully to path 'C:\Program
Files\WindowsPowerShell\Modules\SnippetPx\1.0.5.18'.
VERBOSE: Module 'TypePx' was installed successfully to path 'C:\Program
Files\WindowsPowerShell\Modules\TypePx\2.0.1.20'.


# Get the installed modules
Get-InstalledModule

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0.5.18   SnippetPx                           PSGallery            The SnippetPx module enhances the snippet experience i...
2.0.1.20   TypePx                              PSGallery            The TypePx module adds properties and methods to the m...

```

## <a name="error-scenarios"></a>Chyba scénáře

```powershell

# Below command fails with 'NameShouldNotContainWildcardCharacters,Install-Module'
Install-Module ContosoServe*

# Below command fails with 'VersionRangeAndRequiredVersionCannotBeSpecifiedTogether,Install-Module'
Install-Module ContosoServer -MinimumVersion 1.0 -RequiredVersion 5.0

# Below command fails with 'VersionParametersAreAllowedOnlyWithSingleName,Install-Module'
Install-Module ContosoClient,ContosoServer -RequiredVersion 2.0

# Below command fails with 'VersionParametersAreAllowedOnlyWithSingleName,Install-Module'
Install-Module ContosoClient,ContosoServer -MinimumVersion 2.0

```

