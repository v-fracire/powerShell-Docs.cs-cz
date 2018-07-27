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
# <a name="reporting-on-jea"></a><span data-ttu-id="e3541-102">Vytváření sestav funkce JEA</span><span class="sxs-lookup"><span data-stu-id="e3541-102">Reporting on JEA</span></span>

<span data-ttu-id="e3541-103">Za účelem hlášení o stavu konfigurace JEA, můžete použít:</span><span class="sxs-lookup"><span data-stu-id="e3541-103">In order to report on the state of your JEA configuration, you can use:</span></span>

1. <span data-ttu-id="e3541-104">**Get-PSSessionConfiguration** vrátí seznam všech registrovaných koncových bodů na daném počítači.</span><span class="sxs-lookup"><span data-stu-id="e3541-104">**Get-PSSessionConfiguration** to return a list of all registered endpoints on a given machine.</span></span>
2. <span data-ttu-id="e3541-105">**Get-PSSessionCapability** hlášení o možnostech libovolný daný uživatel má na určitý koncový bod.</span><span class="sxs-lookup"><span data-stu-id="e3541-105">**Get-PSSessionCapability** to report on the capabilities any given user has on a specific endpoint.</span></span>

<span data-ttu-id="e3541-106">Tady je příklad **Get-PSSessionCapability**:</span><span class="sxs-lookup"><span data-stu-id="e3541-106">Here's an example of **Get-PSSessionCapability**:</span></span>

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

<span data-ttu-id="e3541-107">K vytvoření sestavy _akce_ uživatelé trvalo během relace JEA, můžete:</span><span class="sxs-lookup"><span data-stu-id="e3541-107">To report on the _actions_ users took during a JEA session, you can:</span></span>

1. <span data-ttu-id="e3541-108">Povolit záznamy o studiu "over-the-rameno, bude" pro tohoto koncového bodu JEA a prostudovat si adresáři přepisu pro úplný protokol akcí jednotlivých uživatelů</span><span class="sxs-lookup"><span data-stu-id="e3541-108">Enable the "over-the-shoulder" transcripts for that JEA endpoint and consult the transcript directory for a full log of each user's actions</span></span>
2. <span data-ttu-id="e3541-109">Zapnutí protokolování modulu prostředí PowerShell a zkontrolujte protokoly událostí prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3541-109">Turn on PowerShell module logging and inspect the PowerShell event logs.</span></span>