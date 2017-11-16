---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: Get-InstalledScript
ms.openlocfilehash: f35e57cdadd1448bd9032ab007d692003c4cf4a2
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="get-installedscript"></a>Get-InstalledScript

Získá nainstalované v počítači skripty.

## <a name="description"></a>Popis

Rutinu Get-InstalledScript získá nainstalované skriptů prostředí PowerShell v počítači.

Pro každý nainstalovaný skript vrátí Get-InstalledScript PSRepositoryItemInfo objekt, který lze volitelně přesměrovat odinstalační skript pro odinstalaci nainstalovaného skripty.

- Get-InstalledScript můžete filtrovat nainstalované skripty založené na název, verze parametry.
- Get-InstalledScript můžete filtrovat s parametry verze: MinimumVersion, MaximumVersion, RequiredVersion, AllVersions.
  - Tyto parametry se vzájemně vylučují, s výjimkou MinmimumVersion a MaximumVersion.
  - Tyto parametry verze jsou povoleny pouze s názvem jednoho skriptu bez žádné zástupné znaky.
  - Pokud není zadán parametr RequiredVersion, vrátí Get-InstalledScript nejnovější verzi nainstalovaného skript, který je rovna nebo větší než minimální verze zadaná nebo nejnovější verzi skriptu, pokud je zadána žádná minimální verze. 
  - Pokud je zadán parametr RequiredVersion, vrátí Get-InstalledScript pouze verzi nainstalovaného skript, který přesně odpovídá zadaná verze.

## <a name="cmdlet-syntax"></a>Syntaxe rutin

```powershell
Get-Command -Name Get-InstalledScript -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>Referenční informace o rutinách online nápovědy

[Get-InstalledScript](http://go.microsoft.com/fwlink/?LinkId=619790)

## <a name="example-commands"></a>Příklady příkazů

```powershell

# Get all scripts installed using PowerShellGet cmdlets
Get-InstalledScript

# Get a specific installed script
Get-InstalledScript Show-Tree

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0.0      Show-Tree                           PSGallery            Script to show the layout of PowerShell namespaces (Tr...

# Get installed script with wildcards
Get-InstalledScript -Name *Azure*

# Get all versions of an installed script
Get-InstalledScript -Name Connect-O365 -AllVersions

# Get installed script with MinimumVersion
Get-InstalledScript -Name Connect-O365 -MinimumVersion 1.1

# Get installed script with MaximumVersion
Get-InstalledScript -Name Connect-O365 -MaximumVersion 1.6.3

# Get installed script with version range
Get-InstalledScript -Name Connect-O365 -MinimumVersion 1.1 -MaximumVersion 1.6.3

# Get installed script with RequiredVersion
Get-InstalledScript -Name Connect-O365 -RequiredVersion 1.4

# Properties of Get-InstalledScript returned object
Get-InstalledScript Show-Tree | Format-List * -Force

Name                       : Show-Tree
Version                    : 1.0.0
Type                       : Script
Description                : Script to show the layout of PowerShell namespaces (Trees) using ASCII
Author                     : Jeffrey Snover
CompanyName                : jsnover
Copyright                  : (C) Microsoft Corporation. All rights reserved.
PublishedDate              : 2/15/2016 10:15:35 PM
InstalledDate              : 5/4/2016 11:44:13 PM
UpdatedDate                :
LicenseUri                 :
ProjectUri                 :
IconUri                    :
Tags                       : {Nano, PSScript}
Includes                   : {Function, RoleCapability, Command, DscResource...}
PowerShellGetFormatVersion :
ReleaseNotes               :
Dependencies               : {}
RepositorySourceLocation   : https://www.powershellgallery.com/api/v2/
Repository                 : PSGallery
PackageManagementProvider  : NuGet
AdditionalMetadata         : {description, installeddate, tags, PackageManagementProvider...}
InstalledLocation          : C:\Program Files\WindowsPowerShell\Scripts


```

