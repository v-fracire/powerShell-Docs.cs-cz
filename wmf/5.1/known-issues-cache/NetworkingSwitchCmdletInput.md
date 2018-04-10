---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
contributor: vaibch
title: Chyba rutiny správce přepínače sítě
ms.openlocfilehash: 626809513e7a8f1aa2c47a48c74e69ca4077f598
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
<span data-ttu-id="7035a-103">Rutiny správce přepínače sítě můžete použít ke správě přepínače sítě prostřednictvím služby WSMAN.</span><span class="sxs-lookup"><span data-stu-id="7035a-103">The Network Switch Manager cmdlets can be used to manage network switches over WSMAN.</span></span>
<span data-ttu-id="7035a-104">Jsou schopný přijímat hodnoty z kanálů několik rutiny tohoto modulu.</span><span class="sxs-lookup"><span data-stu-id="7035a-104">A few cmdlets of this module are capable of accepting values from pipelines.</span></span>
<span data-ttu-id="7035a-105">Ve verzi Preview 5.1 WMF rutiny, které může přijmout hodnoty z kanálu nepodaří spustit, když nejsou k hodnotám předaným pomocí kanálů.</span><span class="sxs-lookup"><span data-stu-id="7035a-105">In WMF 5.1 Preview, the cmdlets that can accept value from pipeline fail to execute when the values are not passed through pipelines.</span></span>

<span data-ttu-id="7035a-106">Pokud není použit parametr "InputObject", by měly být nadále rutina spustí bez chyb.</span><span class="sxs-lookup"><span data-stu-id="7035a-106">If "InputObject" parameter is not used, the cmdlet should continue to execute without failures.</span></span>

<span data-ttu-id="7035a-107">Tady je seznam ovlivněných rutin, tj. Tyto rutiny může přijmout hodnotu pro parametr "InputObject" z kanálu.</span><span class="sxs-lookup"><span data-stu-id="7035a-107">Here is the list of affected cmdlets i.e. these cmdlets can accept value for "InputObject" parameter from pipeline.</span></span>
<span data-ttu-id="7035a-108">Provádění rutiny se nezdaří, pokud není tato hodnota předaná z kanálu.</span><span class="sxs-lookup"><span data-stu-id="7035a-108">If this value is not passed from pipeline the execution of cmdlet will fail.</span></span>

- <span data-ttu-id="7035a-109">Disable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="7035a-109">Disable-NetworkSwitchEthernetPort</span></span>
- <span data-ttu-id="7035a-110">Enable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="7035a-110">Enable-NetworkSwitchEthernetPort</span></span>
- <span data-ttu-id="7035a-111">Remove-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="7035a-111">Remove-NetworkSwitchEthernetPortIPAddress</span></span>
- <span data-ttu-id="7035a-112">Set-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="7035a-112">Set-NetworkSwitchEthernetPortIPAddress</span></span>
- <span data-ttu-id="7035a-113">Set-NetworkSwitchPortMode</span><span class="sxs-lookup"><span data-stu-id="7035a-113">Set-NetworkSwitchPortMode</span></span>
- <span data-ttu-id="7035a-114">Set-NetworkSwitchPortProperty</span><span class="sxs-lookup"><span data-stu-id="7035a-114">Set-NetworkSwitchPortProperty</span></span>
- <span data-ttu-id="7035a-115">Disable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="7035a-115">Disable-NetworkSwitchFeature</span></span>
- <span data-ttu-id="7035a-116">Enable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="7035a-116">Enable-NetworkSwitchFeature</span></span>
- <span data-ttu-id="7035a-117">Remove-NetworkSwitchVlan</span><span class="sxs-lookup"><span data-stu-id="7035a-117">Remove-NetworkSwitchVlan</span></span>
- <span data-ttu-id="7035a-118">Set-NetworkSwitchVlanProperty</span><span class="sxs-lookup"><span data-stu-id="7035a-118">Set-NetworkSwitchVlanProperty</span></span>

### <a name="resolution"></a><span data-ttu-id="7035a-119">Řešení</span><span class="sxs-lookup"><span data-stu-id="7035a-119">Resolution</span></span>
<span data-ttu-id="7035a-120">Rutiny pracovní dobře, když je hodnota parametru InputObject se předávají do ní prostřednictvím kanálu.</span><span class="sxs-lookup"><span data-stu-id="7035a-120">The cmdlets work fine when the value of InputObject parameter are passed into it through pipeline.</span></span> <span data-ttu-id="7035a-121">Několik příkladů, které fungují pro výše uvedené rutiny jsou:</span><span class="sxs-lookup"><span data-stu-id="7035a-121">A few examples that work for the above cmdlets are:</span></span>

- <span data-ttu-id="7035a-122">Disable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="7035a-122">Disable-NetworkSwitchEthernetPort</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Disable-NetworkSwitchEthernetPort -CimSession $cimSession
```

- <span data-ttu-id="7035a-123">Enable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="7035a-123">Enable-NetworkSwitchEthernetPort</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Enable-NetworkSwitchEthernetPort -CimSession $cimSession
```

- <span data-ttu-id="7035a-124">Remove-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="7035a-124">Remove-NetworkSwitchEthernetPortIPAddress</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Remove-NetworkSwitchEthernetPortIPAddress -CimSession $cimSession
```

- <span data-ttu-id="7035a-125">Set-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="7035a-125">Set-NetworkSwitchEthernetPortIPAddress</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$ipAddress = "192.168.10.1"
$subnetAddress = "255.255.255.0"
$port | Set-NetworkSwitchEthernetPortIPAddress -IpAddress $ipAddress -SubnetAddress $subnetAddress -CimSession $cimSession
```

- <span data-ttu-id="7035a-126">Set-NetworkSwitchPortProperty</span><span class="sxs-lookup"><span data-stu-id="7035a-126">Set-NetworkSwitchPortProperty</span></span>
```powershell
$portProperties = @{Caption = "New Caption"}
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Set-NetworkSwitchPortProperty -Property $portProperties -CimSession $cimSession
```

- <span data-ttu-id="7035a-127">Disable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="7035a-127">Disable-NetworkSwitchFeature</span></span>
```powershell
$feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
$feature | Disable-NetworkSwitchFeature -CimSession $cimSession
```

- <span data-ttu-id="7035a-128">Enable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="7035a-128">Enable-NetworkSwitchFeature</span></span>
```powershell
$feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
$feature | Enable-NetworkSwitchFeature -CimSession $cimSession
```

- <span data-ttu-id="7035a-129">Set-NetworkSwitchVlanProperty</span><span class="sxs-lookup"><span data-stu-id="7035a-129">Set-NetworkSwitchVlanProperty</span></span>
```powershell
$properties = @{Caption = "New Caption"}
$vlan = Get-CimInstance -ClassName CIM_NetworkVlan -Namespace root/interop -CimSession $cimSession | Select-Object -First 1
$vlan | Set-NetworkSwitchVlanProperty -Property $properties -CimSession $cimSession
```