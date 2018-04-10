---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: Find-RoleCapability
ms.openlocfilehash: 89aacd604d54f6a5e9752790be65cc3bcc77c8e1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="find-rolecapability"></a>Find-RoleCapability

Vyhledá role funkce v modulech.

## <a name="description"></a>Popis
Rutinu najít RoleCapability vyhledá role funkce prostředí PowerShell v modulech. Najít RoleCapability vyhledá moduly v registrovaných úložiště.
Pro každou funkci role, která tato rutina vyhledá vrátí objekt PSGetRoleCapabilityInfo. Objekt PSGetRoleCapabilityInfo můžete předat do rutiny Install-Module nainstalovat modul, který obsahuje funkce role.
Možnosti prostředí PowerShell role definovat, které příkazy, aplikace a tak dále jsou k dispozici pro uživatele na koncový bod právě dostatečně správy JEA (). Funkce role jsou definované soubory s příponou .psrc.

- Najít RoleCapability můžete filtrovat s parametry verze: MinimumVersion, RequiredVersion, AllVersions.
  - Tyto parametry se vzájemně vylučují.
  - Tyto parametry verze jsou povoleny pouze s názvem modulu single bez žádné zástupné znaky.
  - Pokud není zadán parametr RequiredVersion, vrátí RoleCapability najít nejnovější verzi modulu, která je rovna nebo větší než minimální verze zadaná nebo nejnovější verzi modulu, pokud je zadána žádná minimální verze.
  - Pokud je zadán parametr RequiredVersion, najít RoleCapability pouze vrátí verzi modul, který přesně odpovídá zadaná verze.
- Najít RoleCapability můžete filtrovat podle metadata modulu s parametrem - značky
- Najít RoleCapability můžete filtrovat podle jazyka vyhledávání podle úložiště s parametrem - filtru.
- Najít RoleCapability můžete filtrovat podle moduly ze všech nebo několika registrované úložišť.

## <a name="cmdlet-syntax"></a>Syntaxe rutin
```powershell
Get-Command -Name Find-RoleCapability -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>Referenční informace o rutinách online nápovědy

[Find-RoleCapability](http://go.microsoft.com/fwlink/?LinkId=718029)

## <a name="example-commands"></a>Příklady příkazů
```powershell

# Find a specific role capability
Find-RoleCapability -Name Maintenance

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Maintenance                         1.5.0      RoleCapModule                       PrivatePSGallery

# Find multiple role capabilities
Find-RoleCapability -Name MyJeaRole, Maintenance

# Find all available role capabilities from all registered repositories
Find-RoleCapability

# Find available role capabilities from few registered repositories
Find-RoleCapability -Repository PSGallery,PrivatePSGallery

# Find all role capabilities in a specified repository
Find-RoleCapability -Repository PSGallery

# Find a role capability defined in a specific module
Find-RoleCapability -Name Maintenance -ModuleName RoleCapModule

# Find role capabilities from all versions of a module
Find-RoleCapability -ModuleName RoleCapModule -AllVersions

# Find role capabilities with module name and MinimumVersion.
Find-RoleCapability -ModuleName RoleCapModule -MinimumVersion 1.1

# Find role capabilities with module name and exact version
Find-RoleCapability -ModuleName RoleCapModule -RequiredVersion 1.4.0

# Find role capabilities defined modules with -Filter based search. -Filter searches in description and module names
Find-RoleCapability -Filter Cookbook
Find-RoleCapability -Filter RBAC

# Find all role capabilities with tags Azure or DSC in module metadata
Find-RoleCapability -Tag Azure, DSC

```