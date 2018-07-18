---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 2fb2e4b0c40322b5ec78fabede22a7e3ecbbd2aa
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093758"
---
# <a name="reporting-on-jea"></a><span data-ttu-id="095e4-102">Vytváření sestav funkce JEA</span><span class="sxs-lookup"><span data-stu-id="095e4-102">Reporting on JEA</span></span>

<span data-ttu-id="095e4-103">Za účelem hlášení o stavu konfigurace JEA, můžete použít:</span><span class="sxs-lookup"><span data-stu-id="095e4-103">In order to report on the state of your JEA configuration, you can use:</span></span>

1. <span data-ttu-id="095e4-104">**Get-PSSessionConfiguration** vrátí seznam všech registrovaných koncových bodů na daném počítači.</span><span class="sxs-lookup"><span data-stu-id="095e4-104">**Get-PSSessionConfiguration** to return a list of all registered endpoints on a given machine.</span></span>
1. <span data-ttu-id="095e4-105">**Get-PSSessionCapability** hlášení o možnostech libovolný daný uživatel má na určitý koncový bod.</span><span class="sxs-lookup"><span data-stu-id="095e4-105">**Get-PSSessionCapability** to report on the capabilities any given user has on a specific endpoint.</span></span>

<span data-ttu-id="095e4-106">Tady je příklad **Get-PSSessionCapability**:</span><span class="sxs-lookup"><span data-stu-id="095e4-106">Here's an example of **Get-PSSessionCapability**:</span></span>

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

<span data-ttu-id="095e4-107">K vytvoření sestavy _akce_ uživatelé trvalo během relace JEA, můžete:</span><span class="sxs-lookup"><span data-stu-id="095e4-107">To report on the _actions_ users took during a JEA session, you can:</span></span>
1. <span data-ttu-id="095e4-108">Povolit záznamy o studiu "over-the-rameno, bude" pro tohoto koncového bodu JEA a prostudovat si adresáři přepisu pro úplný protokol akcí jednotlivých uživatelů</span><span class="sxs-lookup"><span data-stu-id="095e4-108">Enable the "over-the-shoulder" transcripts for that JEA endpoint and consult the transcript directory for a full log of each user's actions</span></span>
2. <span data-ttu-id="095e4-109">Zapnutí protokolování modulu prostředí PowerShell a zkontrolujte protokoly událostí prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="095e4-109">Turn on PowerShell module logging and inspect the PowerShell event logs.</span></span>
