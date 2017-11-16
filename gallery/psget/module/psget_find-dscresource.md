---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: "Najít DscResource"
ms.openlocfilehash: 37ba7925d6f73c453126f25e0818b3f8839d3b3b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="find-dscresource"></a>Najít DscResource

Vyhledá prostředky DSC v modulech.

## <a name="description"></a>Popis

Vyhledá rutinu najít DscResource [konfigurace požadovaného stavu (DSC)](https://msdn.microsoft.com/en-us/PowerShell/dsc/overview) prostředky obsažené v moduly, které odpovídají zadaným kritériím z registrovaných úložiště.
Pro každý modul, který tato rutina vyhledá najít DscResource vrátí objekt PSGetDscResourceInfo, který může vést k instalaci modulu pro instalaci modulů obsahující prostředky, které tato rutina vrací.

DSC je nová platforma pro správu v prostředí Windows PowerShell, který umožňuje nasazení a Správa konfigurační data pro softwaru služby a správu prostředí, ve kterém se tyto služby spuštěny.

Požadované prostředky konfigurace stavu (DSC) poskytují stavební bloky pro konfiguraci DSC. Prostředek zpřístupní vlastnosti, které může být nakonfigurované (schéma) a obsahuje funkce skriptu prostředí PowerShell, které místní Configuration Manager (LCM) žádostí na "jej tak".

Prostředek může model něco jako obecný jako soubor nebo co nastavení serveru služby IIS. Skupiny jako prostředky společně na modul DSC, který slouží k uspořádání všechny požadované soubory v strukturu, která je přenosný a zahrnuje metadata k identifikaci, jak jsou prostředky určena k použití.

- Najít DscResource můžete filtrovat s parametry verze: MinimumVersion, RequiredVersion, AllVersions.
  - Tyto parametry se vzájemně vylučují.
  - Tyto parametry verze jsou povoleny pouze s názvem modulu single bez žádné zástupné znaky.
  - Pokud není zadán parametr RequiredVersion, vrátí DscResource najít nejnovější verzi modulu, která je rovna nebo větší než minimální verze zadaná nebo nejnovější verzi modulu, pokud je zadána žádná minimální verze.
  - Pokud je zadán parametr RequiredVersion, najít DscResource pouze vrátí verzi modul, který přesně odpovídá zadaná verze.
- Najít DscResource můžete filtrovat podle metadata modulu s parametrem - značky
- Najít DscResource můžete filtrovat podle jazyka vyhledávání podle úložiště s parametrem - filtru.
- Najít DscResource můžete filtrovat podle moduly ze všech nebo několika registrované úložišť.

## <a name="cmdlet-syntax"></a>Syntaxe rutin
```powershell
Get-Command -Name Find-DscResource -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>Referenční informace o rutinách online nápovědy

[Najít DscResource](http://go.microsoft.com/fwlink/?LinkId=517196)

## <a name="example-commands"></a>Příklady příkazů
```powershell

# Find a specific DSC Resource
Find-DscResource -Name xIisFeatureDelegation

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
xIisFeatureDelegation               1.10.0.0   xWebAdministration                  PSGallery

# Find all available DSC Resources from all registered repositories
Find-DscResource

# Find a DSC resource by name
Find-DscResource -Name xWebsite

# Find multiple DSC Resources
Find-DscResource -Name xIisHandler, xFirewall

# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking
Find-DscResource -ModuleName xWebAdministration

# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

# Find available DSC Resources from few registered repositories
Find-DscResource -Repository PSGallery,PrivatePSGallery

# Find all DSC Resources in a specified repository
Find-DscResource -Repository PSGallery

# Find DSC Resources from all versions of a module
Find-DscResource -ModuleName xNetworking -AllVersions

# Find DSC Resources with module name and MinimumVersion.
Find-DscResource -ModuleName xNetworking -MinimumVersion 1.1

# Find DSC Resources with module name and exact version
Find-DscResource -ModuleName xNetworking -RequiredVersion 2.1.1

# Find DSC Resources defined modules with -Filter based search. -Filter searches in description and module names
Find-DscResource -Filter Domain

# Find all DSC Resources with tags Azure or DSC in module metadata
Find-DscResource -Tag Azure, DSC

```

