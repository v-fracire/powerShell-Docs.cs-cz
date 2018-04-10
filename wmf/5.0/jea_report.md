---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 2af56be1915c148809f52cd9040c45da160ae0a2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="reporting-on-jea"></a><span data-ttu-id="d1be7-102">Vytváření sestav funkce JEA</span><span class="sxs-lookup"><span data-stu-id="d1be7-102">Reporting on JEA</span></span>
<span data-ttu-id="d1be7-103">Za účelem hlášení o stavu vaší konfigurace JEA, můžete použít:</span><span class="sxs-lookup"><span data-stu-id="d1be7-103">In order to report on the state of your JEA configuration, you can use:</span></span>
1.  <span data-ttu-id="d1be7-104">**Get-PSSessionConfiguration** vrátí seznam všech zaregistrovat koncových bodů na daný počítač.</span><span class="sxs-lookup"><span data-stu-id="d1be7-104">**Get-PSSessionConfiguration** to return a list of all registered endpoints on a given machine.</span></span>
2.  <span data-ttu-id="d1be7-105">**Get-PSSessionCapability** Pokud chcete sestavu podle možností má všechny daného uživatele na konkrétní koncový bod.</span><span class="sxs-lookup"><span data-stu-id="d1be7-105">**Get-PSSessionCapability** to report on the capabilities any given user has on a specific endpoint.</span></span>

<span data-ttu-id="d1be7-106">Tady je příklad **Get-PSSessionCapability**:</span><span class="sxs-lookup"><span data-stu-id="d1be7-106">Here’s an example of **Get-PSSessionCapability**:</span></span>
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

<span data-ttu-id="d1be7-107">K vytvoření sestavy _akce_ uživatelé trvalo během relace JEA, můžete:</span><span class="sxs-lookup"><span data-stu-id="d1be7-107">To report on the _actions_ users took during a JEA session, you can:</span></span>
1. <span data-ttu-id="d1be7-108">Povolit přepisy "over-the osazení" pro tento koncový bod JEA a podívejte se adresáři přepis úplné protokolu akcí jednotlivých uživatelů</span><span class="sxs-lookup"><span data-stu-id="d1be7-108">Enable the "over-the-shoulder" transcripts for that JEA endpoint and consult the transcript directory for a full log of each user's actions</span></span>
2. <span data-ttu-id="d1be7-109">Zapnutí protokolování modulu prostředí PowerShell a zkontrolujte protokoly událostí prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1be7-109">Turn on PowerShell module logging and inspect the PowerShell event logs.</span></span>