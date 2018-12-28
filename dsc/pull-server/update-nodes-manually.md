---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Aktualizovat uzly ze serveru vyžádané replikace
ms.openlocfilehash: 4333a5bf82ef45f22a062942ebe93409433623f5
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403624"
---
# <a name="update-nodes-from-a-pull-server"></a><span data-ttu-id="52629-103">Aktualizovat uzly ze serveru vyžádané replikace</span><span class="sxs-lookup"><span data-stu-id="52629-103">Update Nodes from a Pull Server</span></span>

<span data-ttu-id="52629-104">Následující části se předpokládá, že jste již nastavili serveru vyžádaných replikací s.</span><span class="sxs-lookup"><span data-stu-id="52629-104">The sections below assume that you have already set up a Pull Server.</span></span> <span data-ttu-id="52629-105">Pokud jste nenastavili serveru o přijetí změn, můžete použít následující příručky:</span><span class="sxs-lookup"><span data-stu-id="52629-105">If you have not set up your Pull Server, you can use the following guides:</span></span>

- [<span data-ttu-id="52629-106">Nastavení serveru vyžádané replikace DSC SMB</span><span class="sxs-lookup"><span data-stu-id="52629-106">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="52629-107">Nastavení serveru vyžádané replikace DSC HTTP</span><span class="sxs-lookup"><span data-stu-id="52629-107">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)

<span data-ttu-id="52629-108">Každý cílový uzel je nakonfigurovat ke stažení konfigurace, prostředků a dokonce i oznámit svůj stav.</span><span class="sxs-lookup"><span data-stu-id="52629-108">Each target node can be configured to download configurations, resources, and even report its status.</span></span> <span data-ttu-id="52629-109">Tento článek vám ukáže jak nahrát prostředky, takže jsou k dispozici chcete stahovat a nastavte klienty, aby automaticky stáhnout prostředky.</span><span class="sxs-lookup"><span data-stu-id="52629-109">This article will show you how to upload resources so they are available to be downloaded, and configure clients to download resources automatically.</span></span> <span data-ttu-id="52629-110">Když uzel obdrží přiřazených konfigurací prostřednictvím **o přijetí změn** nebo **Push** (v5), automaticky stáhne všechny prostředky, které konfigurace z umístění zadaného v LCM vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="52629-110">When the Node's receives an assigned Configuration, through **Pull** or **Push** (v5), it automatically downloads any resources required by the Configuration from the location specified in the LCM.</span></span>

## <a name="using-the-update-dscconfiguration-cmdlet"></a><span data-ttu-id="52629-111">Pomocí rutiny Update-DSCConfiguration</span><span class="sxs-lookup"><span data-stu-id="52629-111">Using the Update-DSCConfiguration cmdlet</span></span>

<span data-ttu-id="52629-112">V Powershellu 5.0 [Update-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/update-dscconfiguration) rutiny, vynutí uzel k aktualizaci konfigurace ze serveru vyžádaných gurovaný LCM.</span><span class="sxs-lookup"><span data-stu-id="52629-112">Beginning in PowerShell 5.0, the [Update-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/update-dscconfiguration) cmdlet, forces a Node to update its configuration from the Pull Server configured in the LCM.</span></span>

```powershell
Update-DSCConfiguration -ComputerName "Server01"
```

## <a name="using-invoke-cimmethod"></a><span data-ttu-id="52629-113">Pomocí Invoke CIMMethod</span><span class="sxs-lookup"><span data-stu-id="52629-113">Using Invoke-CIMMethod</span></span>

<span data-ttu-id="52629-114">V Powershellu 4.0, můžete ručně vynutit klienta o přijetí změn aktualizovat jeho konfiguraci pomocí [Invoke CIMMethod](/powershell/module/cimcmdlets/invoke-cimmethod).</span><span class="sxs-lookup"><span data-stu-id="52629-114">In PowerShell 4.0, you can still manually force a Pull Client to update its Configuration using [Invoke-CIMMethod](/powershell/module/cimcmdlets/invoke-cimmethod).</span></span> <span data-ttu-id="52629-115">Následující příklad vytvoří relaci CIM pomocí zadaných přihlašovacích údajů, vyvolá vhodnou metodu CIM a odebere relace.</span><span class="sxs-lookup"><span data-stu-id="52629-115">The following example creates a CIM session with specified credentials, invokes the appropriate CIM method, and removes the session.</span></span>

```powershell
$cimSession = New-CimSession -ComputerName "Server01" -Credential $(Get-Credential)
Invoke-CimMethod -CimSession $cimSession -Namespace 'root/microsoft/windows/desiredstateconfiguration' -Class 'MSFT_DscLocalConfigurationManager' -MethodName 'PerformRequiredConfigurationChecks' -Arguments @{ 'Flags' = [uint32]1 } -Verbose
$cimSession | Remove-CimSession
```

## <a name="see-also"></a><span data-ttu-id="52629-116">Viz také</span><span class="sxs-lookup"><span data-stu-id="52629-116">See Also</span></span>

[<span data-ttu-id="52629-117">PerformRequiredConfigurationChecks</span><span class="sxs-lookup"><span data-stu-id="52629-117">PerformRequiredConfigurationChecks</span></span>](/powershell/dsc/msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks)
