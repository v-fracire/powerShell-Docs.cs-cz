---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 2f05fe96ec792a31fabf3aff0f9e18b40178316c
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893184"
---
# <a name="packagemanagement-cmdlets"></a>Rutiny PackageManagement

Toto je základní PackageManagement pro podporu softwaru zjišťování, instalaci a inventarizaci (SDII). Vyzkoušejte si rutiny pro tyto operace:

- `Find-Package`
- `Find-PackageProvider`
- `Get-Package`
- `Get-PackageProvider`
- `Get-PackageSource`
- `Import-PackageProvider`
- `Install-Package`
- `Install-PackageProvider`
- `Register-PackageSource`
- `Save-Package`
- `Set-PackageSource`
- `Uninstall-Package`
- `Unregister-PackageSource`

PackageManagement je modul Powershellu, můžete provést následující aktualizace PackageManagement sama:

```powershell
Install-Module PackageManagement –Force
```

V takovém případě budete muset znovu zadat relaci Powershellu přejděte do nové verze modulu PackageManagement.

## <a name="find-package-cmdletpowershellmodulepackagemanagementfind-package"></a>[Rutiny Find-Package](/powershell/module/PackageManagement/Find-Package)

Tato rutina umožňuje zjišťování softwarových balíčků ve zdroji k dispozici balíčků pomocí načíst balíček poskytovatelů.

```powershell
# Find all available Windows PowerShell module packages from galleries registered
# with PowerShellGet provider
Find-Package -ProviderName PowerShellGet -Source as source
Find-Package -Name jquery –Provider NuGet -Source http://www.nuget.org/api/v2/

# Find package with name and version
# Here we are assuming that the user already registered nuget.org using
# Register-PackageSource. You can specify either the provider or the source, or
# neither. For the latter, performance may be less optimal as it searches through all
# the providers and registered sources.
Find-Package -Name jquery –Provider NuGet –RequiredVersion 2.1.4 -Source nuget.org
```

## <a name="find-packageprovider-cmdletpowershellmodulepackagemanagementfind-packageprovider"></a>[Najít PackageProvider rutiny](/powershell/module/PackageManagement/Find-PackageProvider)

`Find-PackageProvider` Rutina vyhledá odpovídající PackageManagement poskytovatelů, které jsou k dispozici v zdroje balíčků PowerShellGet zaregistrován. Toto jsou poskytovatelé balíček k dispozici pro instalaci `Install-PackageProvider` rutiny. Ve výchozím nastavení to zahrnuje moduly, které jsou k dispozici v galerii prostředí PowerShell s "PackageManagement" a "Zprostředkovatele" značky.

`Find-PackageProvider` také najde odpovídající zprostředkovatele PackageManagement, které jsou k dispozici v úložišti objektů blob v azure PackageManagement kde používáme poskytovatele boostrapper PackageManagement pro hledání a jejich instalace.

```powershell
#Find all available package providers in PackageManagement azure blob store as well as in PowerShellGallery.com
Find-PackageProvider

#Find all versions of a provider
Find-PackageProvider -Name "Nuget" -AllVersions

#Find a provider from a specified source
Find-PackageProvider -Name "Gistprovider" -Source "PSGallery"
```

## <a name="get-package-cmdletpowershellmodulepackagemanagementget-package"></a>[Rutina Get-Package](/powershell/module/PackageManagement/Get-Package)

Tato rutina vrátí seznam všech softwarových balíčků, které byly nainstalovány pomocí modulu PackageManagement.

```powershell
# Get all the packages installed by Programs provider
Get-Package –Provider Programs

# Get all the packages installed by NuGet provider at c:\test using the dynamic
# parameter destination
Get-Package –Provider NuGet -Destination c:\test
```

## <a name="get-packageprovider-cmdletpowershellmodulepackagemanagementget-packageprovider"></a>[Rutina Get-PackageProvider](/powershell/module/PackageManagement/Get-PackageProvider)

Balíček poskytovatelé, kteří jsou načtené a připravená k použití v místním počítači můžete inventarizovat pomocí rutiny.

```powershell
# Get all currently loaded package providers
Get-PackageProvider

# The following cmdlet will show all the package providers available on the machine (including those that are not loaded):
Get-PackageProvider -ListAvailable
```

## <a name="get-packagesource-cmdletpowershellmodulepackagemanagementget-packagesource"></a>[Rutina Get-PackageSource](/powershell/module/PackageManagement/Get-PackageSource)

Tato rutina načte seznam zdroje balíčků, které jsou registrovány pro balíček zprostředkovatele.

```powershell
# Get all package sources
Get-PackageSource

# Get all package sources for a specific provider
Get-PackageSource –ProviderName PowerShellGet
```

## <a name="import-packageprovider-cmdletpowershellmodulepackagemanagementimport-packageprovider"></a>[Rutina Import-PackageProvider](/powershell/module/PackageManagement/Import-PackageProvider)

Tato rutina přidá poskytovatele balíček správy balíčků do aktuální relace.

```powershell
# Import a package provider from the local machine
Import-PackageProvider –Name MyProvider

#The -Name parameter can be either the name of the provider or the full path to the provider. Currently, we support .dll, .exe and.psm1 for the full path case. If the name of the provider is used for the -Name parameter, then additional version parameters such as -RequiredVersion, -MinimumVersion and -MaximumVersion may be specified. Otherwise, the latest version of the provider will be imported.

#If a package provider is not yet loaded to your system, we can discover and install on-demand. You can use explicit discovery and install cmdlets to do so:
 Find-PackageProvider
 Install-PackageProvider –Name MyProvider

#After installed, follow the Import-PackageProvider to load it to your system.

# Import a specific version of a package provider. PackageManagement supports installations of multiple versions of a package provider using PackageProvider cmdlets (not by bootstrapper provider). You can install another version of a package provider given that you already have one up running by:
Find-PackageProvider –Name "Nuget" -AllVersions
Install-PackageProvider -Name "Nuget" -RequiredVersion "2.8.5.201" -Force
Get-PackageProvider –ListAvailable
Import-PackageProvider –Name "Nuget" -RequiredVersion "2.8.5.201" -Verbose
Import-PackageProvider –Name MyProvider –RequiredVersion xxxx -force
```

## <a name="-install-package-cmdletpowershellmodulepackagemanagementinstall-package"></a>[ Rutina Install-Package](/powershell/module/PackageManagement/Install-Package)

Tato rutina umožňuje instalaci softwarových balíků ve zdroji k dispozici balíčků pomocí načíst balíček poskytovatelů.

```powershell
# Install a package by name.
# NuGet provider requires us to provide the dynamic parameter destination path
# when we use this provider to install. Not all providers will require you to supply
# dynamic parameters for PackageManagement cmdlets.
Install-Package -Name jquery -Source nuget.org -Destination c:\test

# Install a package by piping.
Find-Package -Name jquery –Provider NuGet | Install-Package -Destination c:\test
```

## <a name="install-packageprovider-cmdletpowershellmodulepackagemanagementinstall-packageprovider"></a>[Rutina Install-PackageProvider](/powershell/module/PackageManagement/Install-PackageProvider)

Tato rutina nainstaluje jednu nebo více poskytovatelů balíček správy balíčků.

```powershell
# Install a package provider from the PowerShell Gallery
Install-PackageProvider –Name "Gistprovider" -Verbose

# Install a specified version of a package provider
Find-PackageProvider –Name "Nuget" -AllVersions
Install-PackageProvider -Name "Nuget" -RequiredVersion "2.8.5.201" -Force

# Find a provider and install it
Find-PackageProvider –Name "Gistprovider" | Install-PackageProvider -Verbose

# Install a provider to the current user’s module folder
Install-PackageProvider –Name Gistprovider –Verbose –Scope CurrentUser
```

## <a name="register-packagesource-cmdletpowershellmodulepackagemanagementregister-packagesource"></a>[Rutinu Register-PackageSource](/powershell/module/PackageManagement/Register-PackageSource)

Tato rutina Přidá zdroj balíčku pro zadaný balíček zprostředkovatele.
Každý poskytovatel PackageManagement může mít jednu nebo více zdroje softwaru nebo úložiště. PackageManagement poskytuje rutiny prostředí PowerShell Přidat/odebrat/dotaz na zdroj. Například si můžete zaregistrovat zdroj balíčku NuGet zprostředkovatele:

```powershell
Register-PackageSource -Name "NugetSource" -Location "http://www.nuget.org/api/v2" –ProviderName nuget
```

## <a name="save-package-cmdletpowershellmodulepackagemanagementsave-package"></a>[Rutina Save-Package](/powershell/module/PackageManagement/Save-Package)

Tato rutina uloží balíčky na místním počítači bez instalace.

```powershell
# Saves jquery package to c:\test using NuGetProvider
# Notes that the -Path parameter must point to an existing location
Save-Package -Name jquery –Provider NuGet -Path c:\test

# Save a package by piping.
Find-Package -Name jquery -Source http://www.nuget.org/api/v2/ | Save-Package -Path c:\test
Find-Package -Source c:\test
```

## <a name="set-packagesource-cmdletpowershellmodulepackagemanagementset-packagesource"></a>[Rutina set-PackageSource](/powershell/module/PackageManagement/Set-PackageSource)

Tato rutina se změní informace o existujícím zdroji balíčku.

```powershell
#Set-PackageSource changes the values for a source that has already been registered by running the Register-PackageSource cmdlet. By #running Set-PackageSource, you can change the source name and location.
Set-PackageSource  -Name nuget.org -Location  http://www.nuget.org/api/v2 -NewName nuget2 -NewLocation https://www.nuget.org/api/v2
```

## <a name="uninstall-package-cmdletpowershellmodulepackagemanagementuninstall-package"></a>[Odinstalovat balíček rutiny](/powershell/module/PackageManagement/Uninstall-Package)

Tato rutina odinstaluje balíčky nainstalované na místním počítači.

```powershell
# Uninstall jquery using nuget
Uninstall-Package -Name jquery –Provider NuGet -Destination c:\test

# Uninstall a package with by piping with Get-Package
Get-Package -Name jquery –Provider NuGet -Destination c:\test | Uninstall-Package
```

## <a name="unregister-packagesource-cmdletpowershellmodulepackagemanagementunregister-packagesource"></a>[Zrušit registraci PackageSource rutiny](/powershell/module/PackageManagement/Unregister-PackageSource)

```powershell
# Unregister a package source for the NuGet provider. You can use command Unregister-PackageSource, to disconnect with a repository, and Get-PackageSource, to discover what the repositories are associated with that provider.
Unregister-PackageSource  -Name "NugetSource"
```