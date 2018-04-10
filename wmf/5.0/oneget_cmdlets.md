---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: a282ba375c9ee796c1f3d7923f7478e200cd3b19
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="packagemanagement-cmdlets"></a>Rutiny PackageManagement
Toto je základní PackageManagement na podporu softwaru zjišťování, instalace a inventáře (SDII). Vyzkoušejte rutiny pro tyto operace:
-   Find-Package
-   Find-PackageProvider
-   Get-Package
-   Get-PackageProvider
-   Get-PackageSource
-   Import-PackageProvider
-   Install-Package
-   Install-PackageProvider
-   Register-PackageSource
-   Save-Package
-   Set-PackageSource
-   Uninstall-Package
-   Unregister-PackageSource

PackageManagement je modul prostředí PowerShell, můžete provést následující PackageManagement sám sebe aktualizovat:
```powershell
PS C:\> Install-Module PackageManagement –Force
```
V takovém případě bude muset znovu zadat relaci prostředí PowerShell přepnout na novou verzi PackageManagement.

## <a name="find-package-cmdlethttpstechnetmicrosoftcomlibrarydn890709aspx"></a>[Najít balíček rutiny](https://technet.microsoft.com/library/dn890709.aspx)
Tato rutina umožňuje zjišťování softwarové balíčky v balíčku k dispozici zdroje pomocí načíst zprostředkovatelé balíčku.
```powershell
# Find all available Windows PowerShell module packages from galleries registered
# with PowerShellGet provider
Find-Package -Provider PowerShellGet -Source PSGallery

# Find a package from a provider that is not yet installed
# This will bootstrap NuGet provider and then search for jquery package using NuGet
# with <http://www.nuget.org/api/v2/> as source
Find-Package -Name jquery –Provider NuGet -Source http://www.nuget.org/api/v2/

# Find package with name and version
# Here we are assuming that the user already registered nuget.org using
# Register-PackageSource. You can specify either the provider or the source, or
# neither. For the latter, performance may be less optimal as it searches through all
# the providers and registered sources.
Find-Package -Name jquery –Provider NuGet –RequiredVersion 2.1.4 -Source nuget.org
```

## <a name="find-packageprovider-cmdlethttpstechnetmicrosoftcomlibrarymt676544aspx"></a>[Find-PackageProvider Cmdlet](https://technet.microsoft.com/library/mt676544.aspx)
Rutinu najít PackageProvider najde odpovídající PackageManagement poskytovatelů, které jsou k dispozici v zaregistrována PowerShellGet zdroje balíčků. Jsou to zprostředkovatelé balíčku k dispozici pro instalaci pomocí rutiny Install-PackageProvider. Ve výchozím nastavení to zahrnuje moduly, které jsou k dispozici v galerii prostředí PowerShell s 'PackageManagement' a 'Zprostředkovatel' značky.

Najít PackageProvider také najde odpovídající PackageManagement poskytovatelů, které jsou k dispozici v úložišti objektů blob v azure PackageManagement kde používáme zprostředkovatele boostrapper PackageManagement pro hledání a nainstalujete.
```powershell
#Find all available package providers in PackageManagement azure blob store as well as in PowerShellGallery.com
Find-PackageProvider

#Find all versions of a provider
Find-PackageProvider -Name "Nuget" -AllVersions

#Find a provider from a specified source
Find-PackageProvider -Name "Gistprovider" -Source "PSGallery"
```

## <a name="get-package-cmdlethttpstechnetmicrosoftcomlibrarydn890704aspx"></a>[Get-Package Cmdlet](https://technet.microsoft.com/library/dn890704.aspx)
Tato rutina vrátí seznam všech softwarových balíků, které byly nainstalovány pomocí PackageManagement.
```powershell
# Get all the packages installed by Programs provider
Get-Package –Provider Programs

# Get all the packages installed by NuGet provider at c:\test using the dynamic
# parameter destination
Get-Package –Provider NuGet -Destination c:\test
```

## <a name="get-packageprovider-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890703aspx"></a>[Get-PackageProvider Cmdlet](https://technet.microsoft.com/en-us/library/dn890703.aspx)
Balíček zprostředkovatelé, kteří jsou načíst a připravené k použití v místním počítači může být inventarizován pomocí rutiny.
```powershell
# Get all currently loaded package providers
Get-PackageProvider

# The following cmdlet will show all the package providers available on the machine (including those that are not loaded):
Get-PackageProvider -ListAvailable
```

## <a name="get-packagesource-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890705aspx"></a>[Get-PackageSource Cmdlet](https://technet.microsoft.com/en-us/library/dn890705.aspx)
Tato rutina získá seznam zdroje balíčků, které jsou registrovány pro zprostředkovatele balíčku.
```powershelll
# Get all package sources
Get-PackageSource

# Get all package sources for a specific provider
Get-PackageSource –ProviderName PowerShellGet
```

## <a name="import-packageprovider-cmdlethttpstechnetmicrosoftcomen-uslibrarymt676545aspx"></a>[Import-PackageProvider Cmdlet](https://technet.microsoft.com/en-us/library/mt676545.aspx)
Tato rutina přidá zprostředkovatelé balíček správy balíčků pro aktuální relaci.
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

##<a name="-install-package-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890711aspx"></a>[ Rutina Install-Package](https://technet.microsoft.com/en-us/library/dn890711.aspx)

Tato rutina umožňuje instalaci softwarových balíků v balíčku k dispozici zdroje pomocí načíst zprostředkovatelé balíčku.
```powershell
# Install a package by name.
# NuGet provider requires us to provide the dynamic parameter destination path
# when we use this provider to install. Not all providers will require you to supply
# dynamic parameters for PackageManagement cmdlets.
Install-Package -Name jquery -Source nuget.org -Destination c:\test

# Install a package by piping.
Find-Package -Name jquery –Provider NuGet | Install-Package -Destination c:\test
```

## <a name="install-packageprovider-cmdlethttpstechnetmicrosoftcomen-uslibrarymt676543aspx"></a>[Install-PackageProvider Cmdlet](https://technet.microsoft.com/en-us/library/mt676543.aspx)
Tato rutina nainstaluje jeden nebo více poskytovatelů balíček správy balíčků.
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

## <a name="register-packagesource-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890701aspx"></a>[Register-PackageSource Cmdlet](https://technet.microsoft.com/en-us/library/dn890701.aspx)
Tato rutina Přidá zdroj balíčku pro zadaný balíček zprostředkovatele.
Každý poskytovatel PackageManagement může mít jednu nebo více zdrojů softwaru nebo úložiště. PackageManagement poskytuje rutiny prostředí PowerShell k přidání, odebrání nebo dotazu zdroji. Můžete například zaregistrovat zdroj balíčku NuGet zprostředkovatele:
```powershell
Register-PackageSource -Name "NugetSource" -Location "http://www.nuget.org/api/v2" –ProviderName nuget
```

## <a name="save-package-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890708aspx"></a>[Save-Package Cmdlet](https://technet.microsoft.com/en-us/library/dn890708.aspx)
Tato rutina uloží balíčky do místního počítače bez spuštění instalace.
```powershell
# Saves jquery package to c:\test using NuGetProvider
# Notes that the -Path parameter must point to an existing location
Save-Package -Name jquery –Provider NuGet -Path c:\test

# Save a package by piping.
Find-Package -Name jquery -Source http://www.nuget.org/api/v2/ | Save-Package -Path c:\test
Find-Package -source c:\test
```

## <a name="set-packagesource-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890710aspx"></a>[Set-PackageSource Cmdlet](https://technet.microsoft.com/en-us/library/dn890710.aspx)
Tato rutina změní informace o existujícím zdroji balíčku.
```powershell
#Set-PackageSource changes the values for a source that has already been registered by running the Register-PackageSource cmdlet. By #running Set-PackageSource, you can change the source name and location.
Set-PackageSource  -Name nuget.org -Location  http://www.nuget.org/api/v2 -NewName nuget2 -NewLocation https://www.nuget.org/api/v2
```

## <a name="uninstall-package-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890702aspx"></a>[Uninstall-Package Cmdlet](https://technet.microsoft.com/en-us/library/dn890702.aspx)
Tato rutina odinstaluje balíčky nainstalované v místním počítači.
```powershell
# Uninstall jquery using nuget
Uninstall-Package -Name jquery –Provider NuGet -Destination c:\test

# Uninstall a package with by piping with Get-Package
Get-Package -Name jquery –Provider NuGet -Destination c:\test | Uninstall-Package
```

## <a name="unregister-packagesource-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890707aspx"></a>[Unregister-PackageSource Cmdlet](https://technet.microsoft.com/en-us/library/dn890707.aspx)
```powershell
# Unregister a package source for the NuGet provider. You can use command Unregister-PackageSource, to disconnect with a repository, and Get-PackageSource, to discover what the repositories are associated with that provider.
Unregister-PackageSource  -Name "NugetSource"
```