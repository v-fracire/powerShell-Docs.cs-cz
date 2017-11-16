---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 2c7e718bc518b332cb4303ef73b1bf5c924ca471
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="powershell-module-discovery-install-and-inventory-with-powershellget"></a>Modul prostředí PowerShell zjišťování, instalace a inventáře s PowerShellGet
 
PowerShellGet je zahrnutá v této verzi WMF:
-   Vyhledání modulu můžete filtrovat podle metadata modulu s parametrem - značky
-   Vyhledání modulu můžete filtrovat podle jazyka vyhledávání podle úložiště s parametrem - filtru
-   Můžete najít modul filtr založený na modulu obsah s-příkazového - DscResource a - obsahuje parametry
-   Umožňuje najít DscResource zjišťování jednotlivé prostředky DSC v úložiště
-   Podpora pro instalaci z a publikování do sdílené složky s NuGet

## <a name="example-commands"></a>Příklady příkazů
```powershell
\# Find all modules with tags Azure or DSC
Find-Module -Tag Azure, DSC

\# Find modules with a specific DscResource
Find-Module -DscResource xFirewall

\#Find modules with specific commands
Find-Module -Command Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

\# Find all modules with Dsc resources
Find-Module -Includes DscResource

\# Find all modules with cmdlets
Find-Module -Includes Cmdlet

\# Find all modules with functions
Find-Module -Includes Function

\# Find all DSC resources
Find-DscResource

\# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking

\# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

\# Find modules using -Filter parameter
\# Specified filter value is searched in Name and Description properties
Find-Module -Filter Cookbook -Repository PSGallery
Find-Module -Filter RBAC -Repository PSGallery
```

## <a name="new-features-in-powershellget"></a>Nové funkce v PowerShellGet
-   Podpora verzí vedle sebe na prostředí Windows PowerShell 5.0 nebo novější
-   Podpora instalace závislostí modulu
-   Tři nové rutiny
    -   Get-InstalledModule
    -   Odinstalujte modul
    -   Uložit – modul
    
