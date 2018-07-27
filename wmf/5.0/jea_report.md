---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: cd3338ae305896e282056a871974e5f899ef6ff5
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268574"
---
# <a name="reporting-on-jea"></a>Vytváření sestav funkce JEA

Za účelem hlášení o stavu konfigurace JEA, můžete použít:

1. **Get-PSSessionConfiguration** vrátí seznam všech registrovaných koncových bodů na daném počítači.
2. **Get-PSSessionCapability** hlášení o možnostech libovolný daný uživatel má na určitý koncový bod.

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

1. Povolit záznamy o studiu "over-the-rameno, bude" pro tohoto koncového bodu JEA a prostudovat si adresáři přepisu pro úplný protokol akcí jednotlivých uživatelů
2. Zapnutí protokolování modulu prostředí PowerShell a zkontrolujte protokoly událostí prostředí PowerShell.