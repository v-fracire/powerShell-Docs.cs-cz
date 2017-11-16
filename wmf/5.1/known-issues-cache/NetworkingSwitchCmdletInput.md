---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
contributor: vaibch
title: "Chyba rutiny správce přepínače sítě"
ms.openlocfilehash: d9fcdedbfc7d0c3f68624ed1db6259e04c3d06d1
ms.sourcegitcommit: fee03bb9802222078c8d5f6c8efb0698024406ed
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/27/2017
---
<span data-ttu-id="ef91d-103">Rutiny správce přepínače sítě můžete použít ke správě přepínače sítě prostřednictvím služby WSMAN.</span><span class="sxs-lookup"><span data-stu-id="ef91d-103">The Network Switch Manager cmdlets can be used to manage network switches over WSMAN.</span></span> <span data-ttu-id="ef91d-104">Jsou schopný přijímat hodnoty z kanálů několik rutiny tohoto modulu.</span><span class="sxs-lookup"><span data-stu-id="ef91d-104">A few cmdlets of this module are capable of accepting values from pipelines.</span></span> <span data-ttu-id="ef91d-105">Ve verzi Preview 5.1 WMF rutiny, které může přijmout hodnoty z kanálu nepodaří spustit, když nejsou k hodnotám předaným pomocí kanálů.</span><span class="sxs-lookup"><span data-stu-id="ef91d-105">In WMF 5.1 Preview, the cmdlets that can accept value from pipeline fail to execute when the values are not passed through pipelines.</span></span>

<span data-ttu-id="ef91d-106">Pokud není použit parametr "InputObject", by měly být nadále rutina spustí bez chyb.</span><span class="sxs-lookup"><span data-stu-id="ef91d-106">If "InputObject" parameter is not used, the cmdlet should continue to execute without failures.</span></span>

<span data-ttu-id="ef91d-107">Tady je seznam ovlivněných rutin, tj. Tyto rutiny může přijmout hodnotu pro parametr "InputObject" z kanálu.</span><span class="sxs-lookup"><span data-stu-id="ef91d-107">Here is the list of affected cmdlets i.e. these cmdlets can accept value for "InputObject" parameter from pipeline.</span></span> <span data-ttu-id="ef91d-108">Provádění rutiny se nezdaří, pokud není tato hodnota předaná z kanálu.</span><span class="sxs-lookup"><span data-stu-id="ef91d-108">If this value is not passed from pipeline the execution of cmdlet will fail.</span></span>

- <span data-ttu-id="ef91d-109">Zakázat NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="ef91d-109">Disable-NetworkSwitchEthernetPort</span></span>
- <span data-ttu-id="ef91d-110">Povolit NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="ef91d-110">Enable-NetworkSwitchEthernetPort</span></span>
- <span data-ttu-id="ef91d-111">Odebrat NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="ef91d-111">Remove-NetworkSwitchEthernetPortIPAddress</span></span>
- <span data-ttu-id="ef91d-112">Set-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="ef91d-112">Set-NetworkSwitchEthernetPortIPAddress</span></span>
- <span data-ttu-id="ef91d-113">Set-NetworkSwitchPortMode</span><span class="sxs-lookup"><span data-stu-id="ef91d-113">Set-NetworkSwitchPortMode</span></span>
- <span data-ttu-id="ef91d-114">Set-NetworkSwitchPortProperty</span><span class="sxs-lookup"><span data-stu-id="ef91d-114">Set-NetworkSwitchPortProperty</span></span>
- <span data-ttu-id="ef91d-115">Zakázat NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="ef91d-115">Disable-NetworkSwitchFeature</span></span>
- <span data-ttu-id="ef91d-116">Povolit NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="ef91d-116">Enable-NetworkSwitchFeature</span></span>
- <span data-ttu-id="ef91d-117">Odebrat NetworkSwitchVlan</span><span class="sxs-lookup"><span data-stu-id="ef91d-117">Remove-NetworkSwitchVlan</span></span>
- <span data-ttu-id="ef91d-118">Set-NetworkSwitchVlanProperty</span><span class="sxs-lookup"><span data-stu-id="ef91d-118">Set-NetworkSwitchVlanProperty</span></span>

### <a name="resolution"></a><span data-ttu-id="ef91d-119">Řešení</span><span class="sxs-lookup"><span data-stu-id="ef91d-119">Resolution</span></span>
<span data-ttu-id="ef91d-120">Rutiny pracovní dobře, když je hodnota parametru InputObject se předávají do ní prostřednictvím kanálu.</span><span class="sxs-lookup"><span data-stu-id="ef91d-120">The cmdlets work fine when the value of InputObject parameter are passed into it through pipeline.</span></span> <span data-ttu-id="ef91d-121">Několik příkladů, které fungují pro výše uvedené rutiny jsou:</span><span class="sxs-lookup"><span data-stu-id="ef91d-121">A few examples that work for the above cmdlets are:</span></span>

- <span data-ttu-id="ef91d-122">Zakázat NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="ef91d-122">Disable-NetworkSwitchEthernetPort</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Disable-NetworkSwitchEthernetPort -CimSession $cimSession
```

- <span data-ttu-id="ef91d-123">Povolit NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="ef91d-123">Enable-NetworkSwitchEthernetPort</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Enable-NetworkSwitchEthernetPort -CimSession $cimSession
```

- <span data-ttu-id="ef91d-124">Odebrat NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="ef91d-124">Remove-NetworkSwitchEthernetPortIPAddress</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Remove-NetworkSwitchEthernetPortIPAddress -CimSession $cimSession
```

- <span data-ttu-id="ef91d-125">Set-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="ef91d-125">Set-NetworkSwitchEthernetPortIPAddress</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$ipAddress = "192.168.10.1"
$subnetAddress = "255.255.255.0"
$port | Set-NetworkSwitchEthernetPortIPAddress -IpAddress $ipAddress -SubnetAddress $subnetAddress -CimSession $cimSession
```

- <span data-ttu-id="ef91d-126">Set-NetworkSwitchPortProperty</span><span class="sxs-lookup"><span data-stu-id="ef91d-126">Set-NetworkSwitchPortProperty</span></span>
```powershell
$portProperties = @{Caption = "New Caption"}
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Set-NetworkSwitchPortProperty -Property $portProperties -CimSession $cimSession
```

- <span data-ttu-id="ef91d-127">Zakázat NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="ef91d-127">Disable-NetworkSwitchFeature</span></span>
```powershell
$feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
$feature | Disable-NetworkSwitchFeature -CimSession $cimSession
```

- <span data-ttu-id="ef91d-128">Povolit NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="ef91d-128">Enable-NetworkSwitchFeature</span></span>
```powershell
$feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
$feature | Enable-NetworkSwitchFeature -CimSession $cimSession
```

- <span data-ttu-id="ef91d-129">Set-NetworkSwitchVlanProperty</span><span class="sxs-lookup"><span data-stu-id="ef91d-129">Set-NetworkSwitchVlanProperty</span></span>
```powershell
$properties = @{Caption = "New Caption"}
$vlan = Get-CimInstance -ClassName CIM_NetworkVlan -Namespace root/interop -CimSession $cimSession | Select-Object -First 1
$vlan | Set-NetworkSwitchVlanProperty -Property $properties -CimSession $cimSession
```

