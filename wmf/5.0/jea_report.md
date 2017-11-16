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
# <a name="reporting-on-jea"></a><span data-ttu-id="d1eab-102">Zprávy o JEA</span><span class="sxs-lookup"><span data-stu-id="d1eab-102">Reporting on JEA</span></span>
<span data-ttu-id="d1eab-103">Za účelem hlášení o stavu vaší konfigurace JEA, můžete použít:</span><span class="sxs-lookup"><span data-stu-id="d1eab-103">In order to report on the state of your JEA configuration, you can use:</span></span>
1.  <span data-ttu-id="d1eab-104">**Get-PSSessionConfiguration** vrátí seznam všech zaregistrovat koncových bodů na daný počítač.</span><span class="sxs-lookup"><span data-stu-id="d1eab-104">**Get-PSSessionConfiguration** to return a list of all registered endpoints on a given machine.</span></span>
2.  <span data-ttu-id="d1eab-105">**Get-PSSessionCapability** Pokud chcete sestavu podle možností má všechny daného uživatele na konkrétní koncový bod.</span><span class="sxs-lookup"><span data-stu-id="d1eab-105">**Get-PSSessionCapability** to report on the capabilities any given user has on a specific endpoint.</span></span>

<span data-ttu-id="d1eab-106">Tady je příklad **Get-PSSessionCapability**:</span><span class="sxs-lookup"><span data-stu-id="d1eab-106">Here’s an example of **Get-PSSessionCapability**:</span></span>
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

<span data-ttu-id="d1eab-107">K vytvoření sestavy _akce_ uživatelé trvalo během relace JEA, můžete:</span><span class="sxs-lookup"><span data-stu-id="d1eab-107">To report on the _actions_ users took during a JEA session, you can:</span></span>
1. <span data-ttu-id="d1eab-108">Povolit přepisy "over-the osazení" pro tento koncový bod JEA a podívejte se adresáři přepis úplné protokolu akcí jednotlivých uživatelů</span><span class="sxs-lookup"><span data-stu-id="d1eab-108">Enable the "over-the-shoulder" transcripts for that JEA endpoint and consult the transcript directory for a full log of each user's actions</span></span>
2. <span data-ttu-id="d1eab-109">Zapnutí protokolování modulu prostředí PowerShell a zkontrolujte protokoly událostí prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1eab-109">Turn on PowerShell module logging and inspect the PowerShell event logs.</span></span>

