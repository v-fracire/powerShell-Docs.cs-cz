---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.topic: conceptual
contributor: vaibch
title: Chyba rutiny správce přepínače sítě
ms.openlocfilehash: a0f84c35974b6674faba4b0f19a28bd6e2490a96
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893150"
---
# <a name="network-switch-manager-cmdlets-failure"></a><span data-ttu-id="ee739-103">Chyba rutiny správce přepínače sítě</span><span class="sxs-lookup"><span data-stu-id="ee739-103">Network Switch Manager Cmdlets Failure</span></span>

<span data-ttu-id="ee739-104">Rutiny správce přepínače sítě můžete použít ke správě přepínače sítě prostřednictvím služby WSMAN.</span><span class="sxs-lookup"><span data-stu-id="ee739-104">The Network Switch Manager cmdlets can be used to manage network switches over WSMAN.</span></span>
<span data-ttu-id="ee739-105">Několik rutin tohoto modulu jsou schopny přijímat hodnoty z kanály.</span><span class="sxs-lookup"><span data-stu-id="ee739-105">A few cmdlets of this module are capable of accepting values from pipelines.</span></span>
<span data-ttu-id="ee739-106">WMF 5.1 ve verzi Preview rutin, které může přijmout hodnoty z kanálu nepovedlo se provést při hodnoty neprocházejí kanály.</span><span class="sxs-lookup"><span data-stu-id="ee739-106">In WMF 5.1 Preview, the cmdlets that can accept value from pipeline fail to execute when the values are not passed through pipelines.</span></span>

<span data-ttu-id="ee739-107">Pokud není použit parametr "InputObject", by měl dál rutinu spustit bez chyb.</span><span class="sxs-lookup"><span data-stu-id="ee739-107">If "InputObject" parameter is not used, the cmdlet should continue to execute without failures.</span></span>

<span data-ttu-id="ee739-108">Tady je seznam ovlivněných rutin to znamená tyto rutiny můžete přijmout hodnotu pro parametr "InputObject" z kanálu.</span><span class="sxs-lookup"><span data-stu-id="ee739-108">Here is the list of affected cmdlets i.e. these cmdlets can accept value for "InputObject" parameter from pipeline.</span></span>
<span data-ttu-id="ee739-109">Pokud není tato hodnota předaná z kanálu se nezdaří spuštění rutiny.</span><span class="sxs-lookup"><span data-stu-id="ee739-109">If this value is not passed from pipeline the execution of cmdlet will fail.</span></span>

- <span data-ttu-id="ee739-110">Zakázat NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="ee739-110">Disable-NetworkSwitchEthernetPort</span></span>
- <span data-ttu-id="ee739-111">Povolit NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="ee739-111">Enable-NetworkSwitchEthernetPort</span></span>
- <span data-ttu-id="ee739-112">Odebrat NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="ee739-112">Remove-NetworkSwitchEthernetPortIPAddress</span></span>
- <span data-ttu-id="ee739-113">Set-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="ee739-113">Set-NetworkSwitchEthernetPortIPAddress</span></span>
- <span data-ttu-id="ee739-114">Set-NetworkSwitchPortMode</span><span class="sxs-lookup"><span data-stu-id="ee739-114">Set-NetworkSwitchPortMode</span></span>
- <span data-ttu-id="ee739-115">Set-NetworkSwitchPortProperty</span><span class="sxs-lookup"><span data-stu-id="ee739-115">Set-NetworkSwitchPortProperty</span></span>
- <span data-ttu-id="ee739-116">Zakázat NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="ee739-116">Disable-NetworkSwitchFeature</span></span>
- <span data-ttu-id="ee739-117">Povolit NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="ee739-117">Enable-NetworkSwitchFeature</span></span>
- <span data-ttu-id="ee739-118">Odebrat NetworkSwitchVlan</span><span class="sxs-lookup"><span data-stu-id="ee739-118">Remove-NetworkSwitchVlan</span></span>
- <span data-ttu-id="ee739-119">Set-NetworkSwitchVlanProperty</span><span class="sxs-lookup"><span data-stu-id="ee739-119">Set-NetworkSwitchVlanProperty</span></span>

## <a name="resolution"></a><span data-ttu-id="ee739-120">Řešení</span><span class="sxs-lookup"><span data-stu-id="ee739-120">Resolution</span></span>

<span data-ttu-id="ee739-121">Rutiny pracovní dobře, když je hodnota InputObject parametru jsou předány do něj prostřednictvím kanálu.</span><span class="sxs-lookup"><span data-stu-id="ee739-121">The cmdlets work fine when the value of InputObject parameter are passed into it through pipeline.</span></span> <span data-ttu-id="ee739-122">Je několik příkladů, které fungují pro výše uvedených rutin:</span><span class="sxs-lookup"><span data-stu-id="ee739-122">A few examples that work for the above cmdlets are:</span></span>

- `Disable-NetworkSwitchEthernetPort`

  ```powershell
  $port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
  $port | Disable-NetworkSwitchEthernetPort -CimSession $cimSession
  ```

- `Enable-NetworkSwitchEthernetPort`

  ```powershell
  $port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
  $port | Enable-NetworkSwitchEthernetPort -CimSession $cimSession
  ```

- `Remove-NetworkSwitchEthernetPortIPAddress`

  ```powershell
  $port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
  $port | Remove-NetworkSwitchEthernetPortIPAddress -CimSession $cimSession
  ```

- `Set-NetworkSwitchEthernetPortIPAddress`

  ```powershell
  $port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
  $ipAddress = "192.168.10.1"
  $subnetAddress = "255.255.255.0"
  $port | Set-NetworkSwitchEthernetPortIPAddress -IpAddress $ipAddress -SubnetAddress $subnetAddress -CimSession $cimSession
  ```

- `Set-NetworkSwitchPortProperty`

  ```powershell
  $portProperties = @{Caption = "New Caption"}
  $port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
  $port | Set-NetworkSwitchPortProperty -Property $portProperties -CimSession $cimSession
  ```

- `Disable-NetworkSwitchFeature`

  ```powershell
  $feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
  $feature | Disable-NetworkSwitchFeature -CimSession $cimSession
  ```

- `Enable-NetworkSwitchFeature`

  ```powershell
  $feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
  $feature | Enable-NetworkSwitchFeature -CimSession $cimSession
  ```

- `Set-NetworkSwitchVlanProperty`

  ```powershell
  $properties = @{Caption = "New Caption"}
  $vlan = Get-CimInstance -ClassName CIM_NetworkVlan -Namespace root/interop -CimSession $cimSession | Select-Object -First 1
  $vlan | Set-NetworkSwitchVlanProperty -Property $properties -CimSession $cimSession
  ```