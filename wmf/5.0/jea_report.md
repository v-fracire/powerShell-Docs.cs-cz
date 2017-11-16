---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: f3c218fc668e35fa50047459d8031d77cdf985a2
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="reporting-on-jea"></a>Zprávy o JEA
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

