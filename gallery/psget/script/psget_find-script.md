---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: "Najít skriptu"
ms.openlocfilehash: df62a9934d8013d37bd0083c03f90fa7fa05ac0c
ms.sourcegitcommit: 58371abe9db4b9a0e4e1eb82d39a9f9e187355f9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/05/2017
---
# <a name="find-script"></a>Najít skriptu

Vyhledá soubory skriptu prostředí PowerShell z online galerie odpovídající zadaným kritériím.

## <a name="description"></a>Popis

Najít skriptu vyhledá soubory skriptu z registrovaných úložiště, které odpovídá zadaným kritériím.
Pro každý skript nalezena vrátí najít skriptu PSRepositoryItemInfo objekt, který lze volitelně přesměrovat instalační skript pro instalaci skripty.
Najít skriptu rutina umožňuje zjišťovat soubory skriptu s kritérii vyhledat jiný název, značku, filtr, název příkazu, rozsahu verze, přesnou verzi, všechny verze, včetně jeho závislosti a z určité nebo všech registrovaných úložiště.

- Můžete najít skriptu filtr založený na skript obsah pomocí příkazu - a - obsahuje parametry.
- Najít skriptu můžete filtrovat s parametry verze: MinimumVersion, MaximumVersion, RequiredVersion, AllVersions.
  - Tyto parametry se vzájemně vylučují, s výjimkou MinmimumVersion a MaximumVersion.
  - Tyto parametry verze jsou povoleny pouze s názvem jednoho skriptu bez žádné zástupné znaky.
  - Pokud není zadán parametr RequiredVersion, vrátí skript najít nejnovější verzi skriptu, která je rovna nebo větší než minimální verze zadaná nebo nejnovější verzi skriptu, pokud je zadána žádná minimální verze. 
  - Pokud je zadán parametr RequiredVersion, vrátí skript najít pouze verzi skript, který přesně odpovídá zadaná verze.
- Najít skriptu můžete filtrovat podle metadata skriptu s parametrem - Tag.
- Najít skriptu můžete filtrovat podle jazyka vyhledávání podle úložiště s parametrem - filtru.
- Najít skriptu můžete filtrovat podle skripty ze všech nebo několika registrované úložišť.

**Poznámka:** registrovaná PSRepository by měl mít platný ScriptSourceLocation. Set-PSRepository můžete nastavit hodnotu ScriptSourceLocation.

## <a name="cmdlet-syntax"></a>Syntaxe rutin

```powershell
Get-Command -Name Find-Script -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>Referenční informace o rutinách online nápovědy

[Najít skriptu](http://go.microsoft.com/fwlink/?LinkId=619785)

## <a name="example-commands"></a>Příklady příkazů

```powershell
# Find a script from the registered repository with ScriptSourceLocation
Find-Script Connect-AzureVM

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0        Connect-AzureVM                     PSGallery            This runbook sets up a connection to an Azure vi...

# Find multiple scripts
Find-Script -Name Connect-AzureVM, Show-Tree, Connect-O365

# Find scripts with wildcards in -Name
Find-Script -Name *Azure*

# Find all versions of a script
Find-Script -Name Connect-O365 -AllVersions

# Find a script with -MinimumVersion. 
# With MinimumVersion we can find a script whose version is greate than or equal to the specified MinimumVersion value.
Find-Script Connect-O365 -MinimumVersion 1.4

# Find a script with MaximumVersion
Find-Script -Name Connect-O365 -MaximumVersion 1.6.2

# Find a script with both MinimumVersion and MaximumVersion range.
Find-Script -Name Connect-O365 -MinimumVersion 1.1 -MaximumVersion 1.6.2

# Find a script with exact version
Find-Script -Name Connect-O365 -RequiredVersion 1.5.7

# Find a script with a specific pre-release version
Find-Script -Name Connect-O365 -RequiredVersion 1.3.2-alpha -AllowPrerelease

# Find a script from the specified repository
Find-Script -Name Fabrikam-ServerScript -Repository MyLocalRepo

# Find available scripts from all registered repositories
Find-Script

# Find available scripts from few registered repositories
Find-Script -Repository PSGallery, PrivatePSGallery

# Find a script along with its dependent modules and scripts
Find-Script -Name Connect-AzureVM -IncludeDependencies

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0        Connect-AzureVM                     PSGallery            This runbook sets up a connection to an Azure vi...
1.4.0      Azure                               PSGallery            Microsoft Azure PowerShell - Service Management
1.1.2      Azure.Storage                       PSGallery            Microsoft Azure PowerShell - Storage service cmd...
1.0.8      AzureRM.profile                     PSGallery            Microsoft Azure PowerShell - Profile credential ...

# Find all scripts with workflows
Find-Script -Includes Workflow

# Find all scripts with functions
Find-Script -Includes Function

# Find scripts with specific commands
Find-Script -Command Log-Message
Find-Script -Command Log-Message, Show-Tree -Includes Function
Find-Script -Command Connect-AzureVM -Includes Workflow

# Find scripts with -Filter based search. -Filter searches in description and names
Find-Script -Filter Windows
Find-Script -Filter Azure

# Find all scripts with tags O365 or Nano
Find-Script -Tag O365, Nano

# Properties of Find-Script returned object
Find-Script Show-Tree | Format-List * -Force
Name                       : Show-Tree
Version                    : 1.0.0
Type                       : Script
Description                : Script to show the layout of PowerShell namespaces (Trees) using ASCII
Author                     : Jeffrey Snover
CompanyName                : jsnover
Copyright                  : (C) Microsoft Corporation. All rights reserved.
PublishedDate              : 2/15/2016 10:15:35 PM
InstalledDate              :
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
AdditionalMetadata         : {versionDownloadCount, ItemType, copyright, PackageManagementProvider...}


# Includes property on PSRepositoryItemInfo object
$t = Find-Script -Includes Workflow -Repository INT -Name Fabrikam-ClientScript
$t.Includes

Name                           Value
----                           -----
Function                       {Test-FunctionFromScript_Fabrikam-ClientScript}
RoleCapability                 {}
Command                        {Test-FunctionFromScript_Fabrikam-ClientScript, Test-WorkflowFromScript_Fabrikam-Clie...
DscResource                    {}
Workflow                       {Test-WorkflowFromScript_Fabrikam-ClientScript}
Cmdlet                         {}


```

