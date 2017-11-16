---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: Registrace PSRepository
ms.openlocfilehash: badac5dc1157bbfa79058630c5c2f260d2151bd8
ms.sourcegitcommit: 3720ce4efb6735694cfb53a1b793d949af5d1bc5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2017
---
# <a name="register-psrepository"></a>Registrace PSRepository

Získá registrované úložiště na počítači.

## <a name="description"></a>Popis

Rutinu Register-PSRepository zaregistruje online úložiště pro moduly Powershellu. Po registraci úložiště můžete odkazovat z najít modulu instalace modulu a rutiny modulu publikovat. Registrovaný úložiště se změní výchozí úložiště v modulu vyhledání a instalace modulu. 

Registrovaný úložiště jsou specifické pro uživatele. Nejsou zaregistrovány v rámci celého systému.


## <a name="cmdlet-syntax"></a>Syntaxe rutin

```powershell
Get-Command -Name Register-PSRepository -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a>Referenční informace o rutinách online nápovědy

[Registrace PSRepository](http://go.microsoft.com/fwlink/?LinkID=517129)

## <a name="example-commands"></a>Příklady příkazů

### <a name="register-a-powershell-repository"></a>Zaregistrovat úložiště v prostředí PowerShell
Můžete nakonfigurovat PowerShellGet pro práci s interní úložiště. Po registraci úložiště můžete najít modul a nainstalujte modul s ním pracovat.

```powershell
# Register a default repository
Register-PSRepository –Name DemoRepo –SourceLocation "https://www.myget.org/F/powershellgetdemo/api/v2" –InstallationPolicy Trusted

# Get all of the registered repositories
Name                      InstallationPolicy   SourceLocation
----                      ------------------   --------------
PSGallery                 Untrusted            https://www.powershellgallery.com/api/v2/
DemoRepo                  Trusted              https://www.myget.org/F/powershellgetdemo/api/v2


# Search only the new repository for modules
Find-Module -Repository DemoRepo

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.12.0.0   xActiveDirectory                    DemoRepo             The xActiveDirectory module is originally part of the Windows PowerShell Desired State Configuration (DSC) Resource Kit. This version has been modified for use in Azure. This module contains the xADD...
1.1.1      SomeModule                          DemoRepo             Module description.

# By default, PowerShellGet operates against all registered repositories when none is specified. In this example, the “SomeModule” module is installed from the DemoRepo.
Install-Module SomeModule

# Removing a repository
Unregister-PSRepository DemoRepo
```


### <a name="register-psrepository-and-set-psrepository-cmdlets-with-script-sharing-support"></a>Rutiny Register-PSRepository a Set-PSRepository pomocí skriptu sdílení podpory

Použijte rutinu Register-PSRepository přidat **ScriptSourceLocation** a **ScriptPublishLocation** k PSRepository.

```powershell

# Register an GalleryINT repository with Scripts and Modules support

Register-PSRepository -Name GalleryINT `
                      -SourceLocation https://customgallery.cloudapp.net `
                      -InstallationPolicy Trusted `
                      -Verbose

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet provider must be available in 'C:\Program
Files\PackageManagement\ProviderAssemblies' or 'C:\Users\manikb\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running
'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the NuGet provider now?
[Y] Yes [N] No [S] Suspend [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet provider.
VERBOSE: The specified assembly 'C:\Program Files\PackageManagement\ProviderAssemblies\nuget-anycpu.exe' is installed at top level directory. However it is recommended that the assemblies
should be installed under its ProviderName\Version folder.
VERBOSE: Installing the package 'https://oneget.org/nuget-2.8.5.201.package.swidtag'.
VERBOSE: Installed the package 'nuget' to 'C:\Program Files\PackageManagement\ProviderAssemblies\nuget\2.8.5.201\Microsoft.PackageManagement.NuGetProvider.dll'.
VERBOSE: The provider 'NuGet' has already been imported. Trying to import it again.
VERBOSE: Importing package provider 'NuGet'.
VERBOSE: Performing the operation "Register Module Repository" on target "Module Repository 'GalleryINT' (https://customgallery.cloudapp.net/) in provider 'PowerShellGet'".
VERBOSE: User did not specify the PackageManagement provider name, trying with the provider name 'NuGet'.
VERBOSE: Successfully registered the repository 'GalleryINT' with source location 'https://customgallery.cloudapp.net/api/v2/'.
VERBOSE: Repository details, Name = 'GalleryINT', Location = 'https://customgallery.cloudapp.net/api/v2/'; IsTrusted = 'True'; IsRegistered = 'True'.

# Get the registered repository details
Get-PSRepository -Name GalleryINT

Name                      InstallationPolicy   SourceLocation
----                      ------------------   --------------
GalleryINT                 Trusted              https://customgallery.cloudapp.net/api/v2/


Get-PSRepository -Name GalleryINT | Format-List * -Force

Name : GalleryINT
SourceLocation : https://customgallery.cloudapp.net/api/v2/
Trusted : True
Registered : True
InstallationPolicy : Trusted
PackageManagementProvider : NuGet
PublishLocation : https://customgallery.cloudapp.net/api/v2/package/
ScriptSourceLocation : https://customgallery.cloudapp.net/api/v2/items/psscript/
ScriptPublishLocation : https://customgallery.cloudapp.net/api/v2/package/
ProviderOptions : {}

```

