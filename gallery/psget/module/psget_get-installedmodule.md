---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: Get-InstalledModule
ms.openlocfilehash: 6f485d04503ea6d9a51a68ae7ec3d0dc2e6facab
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="get-installedmodule"></a>Get-InstalledModule

Získá nainstalované moduly v počítači.

## <a name="description"></a>Popis

Rutinu Get-InstalledModule získá nainstalované moduly Powershellu na počítači, které byly nainstalovány pomocí rutiny Install-Module.

Pro každý nainstalovaný modul Get-InstalledModule vrátí PSRepositoryItemInfo objekt, který lze volitelně přesměrovat k odinstalaci modulu pro odinstalaci nainstalované moduly.

- Get-InstalledModule lze filtrovat na základě názvu, parametry verze nainstalované moduly.
- Get-InstalledModule můžete filtrovat s parametry verze: MinimumVersion, MaximumVersion, RequiredVersion, AllVersions.
  - Tyto parametry se vzájemně vylučují, s výjimkou MinmimumVersion a MaximumVersion.
  - Tyto parametry verze jsou povoleny pouze s názvem modulu single bez žádné zástupné znaky.
  - Pokud není zadán parametr RequiredVersion, vrátí Get-InstalledModule nejnovější verzi nainstalovaný modul, která je rovna nebo větší než minimální verze zadaná nebo nejnovější verzi modulu, pokud je zadána žádná minimální verze. 
  - Pokud je zadán parametr RequiredVersion, vrátí Get-InstalledModule pouze verzi nainstalovaný modul, který přesně odpovídá zadaná verze.

## <a name="cmdlet-syntax"></a>Syntaxe rutin
```powershell
Get-Command -Name Get-InstalledModule -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>Referenční informace o rutinách online nápovědy

[Get-InstalledModule](http://go.microsoft.com/fwlink/?LinkId=526863)

## <a name="example-commands"></a>Příklady příkazů

```powershell

# Get all modules installed using PowerShellGet cmdlets
Get-InstalledModule

# Get a specific installed module
Get-InstalledModule DJoin

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0        DJoin                               PSGallery            This is a PowerShell frontend to the DJOIN.exe c...

# Get installed module with wildcards
Get-InstalledModule -Name AzureRM*

# Get all versions of an installed module
Get-InstalledModule -Name AzureRM.Automation -AllVersions

# Get installed module with MinimumVersion
Get-InstalledModule -Name AzureRM.Automation -MinimumVersion 1.0.0

# Get installed module with MaximumVersion
Get-InstalledModule -Name AzureRM.Automation -MaximumVersion 1.0.8

# Get installed module with version range
Get-InstalledModule -Name AzureRM.Automation -MinimumVersion 1.0.0 -MaximumVersion 1.0.8

# Get installed module with RequiredVersion
Get-InstalledScript -Name AzureRM.Automation -RequiredVersion 1.0.3

# Properties of Get-InstalledModule returned object
Get-InstalledModule DJoin | Format-List * -Force

Name                       : DJoin
Version                    : 1.0
Type                       : Module
Description                : This is a PowerShell frontend to the DJOIN.exe command which provides better
                             discoverability and usability.
Author                     : Jeffrey Snover
CompanyName                : jsnover
Copyright                  : (C) Microsoft Corporation. All rights reserved.
PublishedDate              : 2/15/2016 7:12:37 PM
InstalledDate              : 4/5/2016 4:13:39 PM
UpdatedDate                :
LicenseUri                 :
ProjectUri                 :
IconUri                    :
Tags                       : {Nano, PSModule}
Includes                   : {Function, RoleCapability, Command, DscResource...}
PowerShellGetFormatVersion :
ReleaseNotes               :
Dependencies               : {}
RepositorySourceLocation   : https://www.powershellgallery.com/api/v2/
Repository                 : PSGallery
PackageManagementProvider  : NuGet
AdditionalMetadata         : {description, installeddate, tags, PackageManagementProvider...}
InstalledLocation          : C:\Program Files\WindowsPowerShell\Modules\DJoin\1.0

```



## <a name="installeddate-and-updateddate-properties-in-psgetrepositoryiteminfo-object"></a>InstalledDate a UpdatedDate vlastnosti v objektu PSGetRepositoryItemInfo

    During the install operation:
        InstalledDate: current DateTime (Get-Date) value
        UpdatedDate: null

    During the Update operation:
        InstalledDate: InstalledDate from the previous installation otherwise current DateTime (Get-Date) value
        UpdatedDate: current DateTime (Get-Date) value

```powershell
Install-Module -Name ContosoServer -RequiredVersion 1.0 -Repository INT
Get-InstalledModule -Name ContosoServer | Format-Table Name, InstalledDate, UpdatedDate

Name          InstalledDate         UpdatedDate
----          -------------         -----------
ContosoServer 2/29/2016 11:59:14 AM


\Update-Module -Name ContosoServer
Get-InstalledModule -Name ContosoServer | Format-Table Name, InstalledDate, UpdatedDate

Name          InstalledDate         UpdatedDate
----          -------------         -----------
ContosoServer 2/29/2016 11:59:14 AM 2/29/2016 12:00:15 PM
```

