---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 32f8e20889ddc526def4b925e8d0761a2e851e19
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="unified-and-consistent-state-and-status-representation"></a>Jednotné a konzistentní stav a stav reprezentace

Řadu vylepšení byly provedeny v této verzi pro automatizaci vytvořené LCM stav a stav DSC. Patří mezi ně jednotné a konzistentní stav a stav vyjádření, vlastnost datetime spravovatelných objektů stav vrácen rutinou Get-DscConfigurationStatus a rozšířené vlastnosti podrobností LCM stav vrácený Get-DscLocalConfigurationManager rutiny.

Reprezentace LCM stav a stav operace DSC jsou kdykoli znovu spustit a jednotná podle následujících pravidel:
1.  Notprocessed prostředků neovlivní LCM stav a stav DSC.
2.  LCM zastavit zpracování další prostředky, jakmile narazí na prostředek, který požaduje restartování.
3.  Na prostředek, který požaduje restartování není v požadovaném stavu, dokud se ve skutečnosti stane restartování.
4.  Po zjištění na prostředek, který selže, LCM uchová zpracování další prostředky, dokud nejsou závislé na jednu selhání.
5.  Celkový stav, který vrátila Rutina Get-DscConfigurationStatus je supertřídou sada stavu všech prostředků.
6.  Stav PendingReboot je nadmnožinou PendingConfiguration stavu.

Následující tabulka znázorňuje výsledné stav a stav souvisejících vlastností v rámci několik typické scénáře.

| **Scénář**                    | **LCMState\***       | **Stav** | **Požadovaný restart**  | **ResourcesInDesiredState**  | **ResourcesNotInDesiredState** |
|---------------------------------|----------------------|------------|---------------|------------------------------|--------------------------------|
| S**^**                          | Nečinnosti                 | Úspěch    | $false        | S                            | $null                          |
| F**^**                          | PendingConfiguration | Chyba    | $false        | $null                        | F                              |
| S, F                             | PendingConfiguration | Chyba    | $false        | S                            | F                              |
| F, S                             | PendingConfiguration | Chyba    | $false        | S                            | F                              |
| S<sub>1</sub>, F, S<sub>2</sub> | PendingConfiguration | Chyba    | $false        | S<sub>1</sub>, S<sub>2</sub> | F                              |
| F<sub>1</sub>, S, F<sub>2</sub> | PendingConfiguration | Chyba    | $false        | S                            | F<sub>1</sub>, F<sub>2</sub>   |
| S, r                            | PendingReboot        | Úspěch    | $true         | S                            | R                              |
| F, r                            | PendingReboot        | Chyba    | $true         | $null                        | F, r                           |
| r, S                            | PendingReboot        | Úspěch    | $true         | $null                        | R                              |
| r, F                            | PendingReboot        | Úspěch    | $true         | $null                        | R                              |

^ S<sub>i</sub>: řadu prostředky, které bylo úspěšně použito F<sub>i</sub>: řadu prostředky, které použije neúspěšně r: A prostředků, které vyžadují restartování:\*

```powershell
$LCMState = (Get-DscLocalConfigurationManager).LCMState
$Status = (Get-DscConfigurationStatus).Status

$RebootRequested = (Get-DscConfigurationStatus).RebootRequested

$ResourcesInDesiredState = (Get-DscConfigurationStatus).ResourcesInDesiredState

$ResourcesNotInDesiredState = (Get-DscConfigurationStatus).ResourcesNotInDesiredState
```
## <a name="enhancement-in-get-dscconfigurationstatus-cmdlet"></a>Vylepšení v rutině Get-DscConfigurationStatus

Rutina Get-DscConfigurationStatus v této verzi se provedly několik vylepšení. Vlastnost počátečním objektů vrácený rutinu dříve, je typu String. Nyní je typu datum a čas, který umožňuje komplexní, výběru a filtrování snadnější podle vnitřní vlastnosti objektu data a času.
```powershell
(Get-DscConfigurationStatus).StartDate | fl \*
DateTime : Friday, November 13, 2015 1:39:44 PM
Date : 11/13/2015 12:00:00 AM
Day : 13
DayOfWeek : Friday
DayOfYear : 317
Hour : 13
Kind : Local
Millisecond : 886
Minute : 39
Month : 11
Second : 44
Ticks : 635830187848860000
TimeOfDay : 13:39:44.8860000
Year : 2015
```

Následuje příklad, který vrátí že všechny záznamy operaci DSC došlo ve stejný den v týdnu jako dnes.
```powershell
(Get-DscConfigurationStatus –All) | where { $\_.startdate.dayofweek -eq (Get-Date).DayOfWeek }
```

Tím se vyloučí záznamy operací, které nebyly provedeny změny konfigurace uzlu (tj. pouze operace čtení). Proto Test-DscConfiguration operace Get-DscConfiguration jsou již zfalšované v nevrátil z rutiny Get-DscConfigurationStatus objekty.
Zaznamenává meta operace nastavení konfigurace se přidá k návratu rutiny Get-DscConfigurationStatus.

Tady je příklad výsledku vrácený z Get-DscConfigurationStatus – všechny rutiny.
```powershell
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
Nové pole LCMStateDetail se přidá do objekt vrácený z rutiny Get-DscLocalConfigurationManager. V tomto poli se zaplní při LCMState je "Zaneprázdněn". Se dá načíst pomocí následující rutiny:
```powershell
(Get-DscLocalConfigurationManager).LCMStateDetail
```

Následuje příklad výstupu nepřetržitého monitorování v konfiguraci, která vyžaduje dvě restartování na vzdáleném uzlu.
```powershell
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

