---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 7982acc111e95b4167f948314f176d53f39d3620
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218718"
---
# <a name="reporting-on-jea"></a>Vytváření sestav funkce JEA
Za účelem hlášení o stavu vaší konfigurace JEA, můžete použít:
1.  **Get-PSSessionConfiguration** vrátí seznam všech zaregistrovat koncových bodů na daný počítač.
2.  **Get-PSSessionCapability** Pokud chcete sestavu podle možností má všechny daného uživatele na konkrétní koncový bod.

Tady je příklad **Get-PSSessionCapability**:
```powershell
Get-PSSessionCapability -ConfigurationName Maintenance -Username "CONTOSO\JohnDoe"

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           clear -> Clear-Host
Alias           cls -> Clear-Host
Alias           exsn -> Exit-PSSession
Alias           gcm -> Get-Command
Alias           measure -> Measure-Object
Alias           select -> Select-Object
Function        Clear-Host
Function        Exit-PSSession
Function        Get-Command
Function        Get-FormatData
Function        Get-Help
Function        Get-UserInfo
Function        Measure-Object
Function        Out-Default
Function        Select-Object
Cmdlet          Restart-Service                                    3.0.0.0 Microsof...


```

K vytvoření sestavy _akce_ uživatelé trvalo během relace JEA, můžete:
1. Povolit přepisy "over-the osazení" pro tento koncový bod JEA a podívejte se adresáři přepis úplné protokolu akcí jednotlivých uživatelů
2. Zapnutí protokolování modulu prostředí PowerShell a zkontrolujte protokoly událostí prostředí PowerShell.
