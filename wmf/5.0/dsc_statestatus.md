---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: bed1186c10082bbdac7249503bf623678f13fccd
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39267935"
---
# <a name="unified-and-consistent-state-and-status-representation"></a>Jednotné vyjádření stavu

Řadu vylepšení byly provedeny v této verzi za účelem automatizace založená LCM stavu a statusu DSC. Patří mezi ně jednotné stavu a statusu reprezentace, spravovat data a času vlastnost stavu objektů vrácených podle `Get-DscConfigurationStatus` rutiny a vylepšené LCM stavu podrobnosti vlastnosti vrácené `Get-DscLocalConfigurationManager` rutiny.

Vyjádření stavu LCM a stav operace DSC se znovu obrácena pozornost a unified podle následujících pravidel:

1. Notprocessed prostředků neovlivní LCM stavu a statusu DSC.
2. LCM zastavení zpracování další prostředky, jakmile narazí na prostředek, který vyžaduje restartování.
3. Prostředek, který požaduje restartování není v požadovaném stavu, dokud se ve skutečnosti stane restartování.
4. Po zjištění prostředek, který selže, LCM zajišťuje zpracování další prostředky, dokud nejsou závislé na selhání jedné.
5. Celkový stav vrácený `Get-DscConfigurationStatus` rutina je super sadu stavu všechny prostředky.
6. Stav PendingReboot je nadmnožinou PendingConfiguration stavu.

Následující tabulka uvádí, výsledné stavy souvisejících vlastností v rámci několika typické scénáře.

| Scénář                        | LCMState             | Stav     | Požadováno restartování | ResourcesInDesiredState   | ResourcesNotInDesiredState |
|---------------------------------|----------------------|------------|---------------|------------------------------|--------------------------------|
| S**^**                          | Nečinnosti                 | Úspěch    | $false        | S                            | $null                          |
| F**^**                          | PendingConfiguration | Chyba    | $false        | $null                        | F                              |
| S,F                             | PendingConfiguration | Chyba    | $false        | S                            | F                              |
| F,S                             | PendingConfiguration | Chyba    | $false        | S                            | F                              |
| S<sub>1</sub>, F, S<sub>2</sub> | PendingConfiguration | Chyba    | $false        | S<sub>1</sub>, S<sub>2</sub> | F                              |
| F<sub>1</sub>, S, F<sub>2</sub> | PendingConfiguration | Chyba    | $false        | S                            | F<sub>1</sub>, F<sub>2</sub>   |
| S, r                            | PendingReboot        | Úspěch    | $true         | S                            | r                              |
| F, r                            | PendingReboot        | Chyba    | $true         | $null                        | F, r                           |
| r, S                            | PendingReboot        | Úspěch    | $true         | $null                        | r                              |
| r, F                            | PendingReboot        | Úspěch    | $true         | $null                        | r                              |

- S<sub>můžu</sub>: řadu prostředků, které byly úspěšně použity.
- F<sub>můžu</sub>: řadu prostředků, které se použijí neúspěšně
- r: prostředek, který vyžaduje restartování

```powershell
$LCMState = (Get-DscLocalConfigurationManager).LCMState
$Status = (Get-DscConfigurationStatus).Status

$RebootRequested = (Get-DscConfigurationStatus).RebootRequested

$ResourcesInDesiredState = (Get-DscConfigurationStatus).ResourcesInDesiredState

$ResourcesNotInDesiredState = (Get-DscConfigurationStatus).ResourcesNotInDesiredState
```

## <a name="enhancement-in-get-dscconfigurationstatus-cmdlet"></a>Vylepšení v rutině Get-DscConfigurationStatus

Bylo provedeno několik vylepšení na `Get-DscConfigurationStatus` rutiny v této verzi. Vlastnost StartDate objektů vrací rutina dříve, je typu řetězec. Nyní je typu datum a čas, který umožňuje komplexní, výběr a filtrování snadněji založené na vnitřní vlastnosti objektu data a času.

```powershell
(Get-DscConfigurationStatus).StartDate | Format-List *

DateTime    : Friday, November 13, 2015 1:39:44 PM
Date        : 11/13/2015 12:00:00 AM
Day         : 13
DayOfWeek   : Friday
DayOfYear   : 317
Hour        : 13
Kind        : Local
Millisecond : 886
Minute      : 39
Month       : 11
Second      : 44
Ticks       : 635830187848860000
TimeOfDay   : 13:39:44.8860000
Year        : 2015
```

Následující příklad vrátí všechny záznamy operace DSC, ke kterým došlo ve stejný den v týdnu jako aktuální den.

```powershell
(Get-DscConfigurationStatus –All) | Where-Object { $_.startdate.dayofweek -eq (Get-Date).DayOfWeek }
```

Záznamy operací, které nelze provést změny konfigurace uzlu (například pouze operace čtení) jsou odstraněny. Proto `Test-DscConfiguration`, `Get-DscConfiguration` operace jsou již zfalšované v objektů vrácených z `Get-DscConfigurationStatus` rutiny. Záznamy meta operace nastavení konfigurace se přidá do návrat `Get-DscConfigurationStatus` rutiny.

Tady je příklad výsledku vrácený z `Get-DscConfigurationStatus –All` rutiny.

```output
All configuration operations:

Status StartDate Type RebootRequested
------ --------- ---- ---------------
Success 11/13/2015 11:38:16 AM Consistency False
Success 11/13/2015 11:23:16 AM Reboot False
Success 11/13/2015 11:21:43 AM Reboot True
Success 11/13/2015 11:20:44 AM Initial True
Success 11/13/2015 11:20:44 AM LocalConfigurationManager False
```

## <a name="enhancement-in-get-dsclocalconfigurationmanager-cmdlet"></a>Vylepšení v rutině Get-DscLocalConfigurationManager

Přidání nového pole LCMStateDetail pro objekt vrácený z `Get-DscLocalConfigurationManager` rutiny. Toto pole se vyplní po LCMState "Zaneprázdněn". Se dá načíst pomocí následující rutiny:

```powershell
(Get-DscLocalConfigurationManager).LCMStateDetail
```

Tady je příklad výstupu nepřetržitého monitorování v konfiguraci, která vyžaduje dvě restartování na vzdáleném uzlu.

```output
Start a configuration that requires two reboots

Monitor LCM State:
LCM State: Busy, LCM is applying a new configuration.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: Idle,
LCM State: Busy, LCM is performing a consistency check.
LCM State: Idle,
```