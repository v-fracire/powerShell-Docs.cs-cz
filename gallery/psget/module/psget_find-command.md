---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: Najít – příkaz
ms.openlocfilehash: 26ddf4824816db245131a0fc95b7d2a88bef8f4c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="find-command"></a>Najít – příkaz

Vyhledá příkazy prostředí PowerShell v modulech.

## <a name="description"></a>Popis
Najít – příkaz rutina vyhledá příkazy prostředí PowerShell jako rutiny, aliasy, funkce a pracovní postupy. Najít – příkaz vyhledá moduly v registrovaných úložiště.
U každého příkazu, který tato rutina vyhledá vrátí objekt PSGetCommandInfo. Objekt PSGetCommandInfo můžete předat do rutiny Install-Module nainstalovat modul, který obsahuje příkaz.

- Najít – příkaz můžete filtrovat s parametry verze: MinimumVersion, RequiredVersion, AllVersions.
  - Tyto parametry se vzájemně vylučují.
  - Tyto parametry verze jsou povoleny pouze s názvem modulu single bez žádné zástupné znaky.
  - Pokud není zadán parametr RequiredVersion, vrátí příkaz najít nejnovější verzi modulu, která je rovna nebo větší než minimální verze zadaná nebo nejnovější verzi modulu, pokud je zadána žádná minimální verze.
  - Pokud je zadán parametr RequiredVersion, najít – příkaz vrátí jenom verzi modul, který přesně odpovídá zadaná verze.
- Najít – příkaz můžete filtrovat podle metadata modulu s parametrem - značky
- Najít – příkaz můžete filtrovat podle jazyka vyhledávání podle úložiště s parametrem - filtru.
- Najít – příkaz můžete filtrovat podle moduly ze všech nebo několika registrované úložišť.

## <a name="cmdlet-syntax"></a>Syntaxe rutin
```powershell
Get-Command -Name Find-Command -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>Referenční informace o rutinách online nápovědy

[Najít – příkaz](http://go.microsoft.com/fwlink/?LinkId=733636)

## <a name="example-commands"></a>Příklady příkazů
```powershell

# Find a specific command
Find-Command -Name Get-ScriptAnalyzerRule

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Get-ScriptAnalyzerRule              1.5.0      PSScriptAnalyzer                    PSGallery

# Find multiple commands
Find-Command -Name Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

# Find all available commands from all registered repositories
Find-Command

# Find available commands from few registered repositories
Find-Command -Repository PSGallery,PrivatePSGallery

# Find all commands in a specified repository
Find-Command -Repository PSGallery

# Find a command defined in a specific module
Find-Command -Name Get-ScriptAnalyzerRule -Module PSScriptAnalyzer

# Find commands from all versions of a module
Find-Command -ModuleName PSReadline -AllVersions

# Find commands with module name and MinimumVersion.
Find-Command -ModuleName PSReadline -MinimumVersion 1.1

# Find commands with module name and exact version
Find-Command -ModuleName AzureRM -RequiredVersion 1.4.0

# Find commands defined modules with -Filter based search. -Filter searches in description and module names
Find-Command -Filter Cookbook
Find-Command -Filter RBAC

# Find all commands with tags Azure or DSC in module metadata
Find-Command -Tag Azure, DSC

```