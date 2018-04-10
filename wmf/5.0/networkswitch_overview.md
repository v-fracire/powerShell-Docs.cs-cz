---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 2b6b81d250c3d745f3ab21ebadb9a657583638b0
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="network-switch-management-with-powershell"></a><span data-ttu-id="29581-102">Použití PowerShellu ke správě síťového přepínače</span><span class="sxs-lookup"><span data-stu-id="29581-102">Network Switch Management with PowerShell</span></span>

<span data-ttu-id="29581-103">**Get-NetworkSwitchEthernetPort** rutina nyní vrátí následující doplňkové informace s instancemi:</span><span class="sxs-lookup"><span data-stu-id="29581-103">The **Get-NetworkSwitchEthernetPort** cmdlet now returns the following additional information with instances:</span></span>

- <span data-ttu-id="29581-104">IP adresa – IP adresa přidružená port</span><span class="sxs-lookup"><span data-stu-id="29581-104">IPAddress – the IP address associated with the port</span></span>
- <span data-ttu-id="29581-105">PortMode – režim portu: přístup, postup nebo trunk</span><span class="sxs-lookup"><span data-stu-id="29581-105">PortMode – the port mode: access, route, or trunk</span></span>
- <span data-ttu-id="29581-106">AccessVLAN – ID sítě VLAN přidružené tento port v přístupovém režimu</span><span class="sxs-lookup"><span data-stu-id="29581-106">AccessVLAN – the ID of the VLAN associated with this port in access mode</span></span>
- <span data-ttu-id="29581-107">TrunkedVLANList – seznam ID sítě VLAN přiřazený k tomuto portu v páteřním režimu</span><span class="sxs-lookup"><span data-stu-id="29581-107">TrunkedVLANList – a list of IDs of VLANs associated with this port in trunk mode</span></span>

## <a name="fundamental-network-switch-management-with-windows-powershell"></a><span data-ttu-id="29581-108">Správa přepínač základní sítě pomocí prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="29581-108">Fundamental network switch management with Windows PowerShell</span></span>

<span data-ttu-id="29581-109">Rutiny síťového přepínače, ve WMF 5.0, umožňují použít přepínač virtuální sítě LAN (VLAN) a základní konfigurací portu síťového přepínače vrstvy 2 na Windows Server 2012 R2 logo certified síťové přepínače.</span><span class="sxs-lookup"><span data-stu-id="29581-109">The Network Switch cmdlets, introduced in WMF 5.0, enable you to apply switch, virtual LAN (VLAN), and basic Layer 2 network switch port configuration to Windows Server 2012 R2 logo-certified network switches.</span></span> <span data-ttu-id="29581-110">Microsoft stále snaží podpora [Datacenter Abstraction](http://technet.microsoft.com/cloud/dal.aspx) vize Layer (DAL) a zobrazit hodnotu pro naše zákazníky a partnery v tomto prostor.</span><span class="sxs-lookup"><span data-stu-id="29581-110">Microsoft remains committed to supporting the [Datacenter Abstraction](http://technet.microsoft.com/cloud/dal.aspx) Layer (DAL) vision, and to show value for our customers and partners in this space.</span></span> <span data-ttu-id="29581-111">Pomocí těchto rutin můžete provést:</span><span class="sxs-lookup"><span data-stu-id="29581-111">Using these cmdlets you can perform:</span></span>

- <span data-ttu-id="29581-112">Globální přepínači konfigurace, jako například:</span><span class="sxs-lookup"><span data-stu-id="29581-112">Global switch configuration, such as:</span></span>
    - <span data-ttu-id="29581-113">Název hostitele sady</span><span class="sxs-lookup"><span data-stu-id="29581-113">Set host name</span></span>
    - <span data-ttu-id="29581-114">Hlavička set přepínače</span><span class="sxs-lookup"><span data-stu-id="29581-114">Set switch banner</span></span>
    - <span data-ttu-id="29581-115">Trvalá konfigurace</span><span class="sxs-lookup"><span data-stu-id="29581-115">Persist configuration</span></span>
    - <span data-ttu-id="29581-116">Povolení nebo zakázání funkce</span><span class="sxs-lookup"><span data-stu-id="29581-116">Enable or disable feature</span></span>

- <span data-ttu-id="29581-117">Konfigurace sítě VLAN:</span><span class="sxs-lookup"><span data-stu-id="29581-117">VLAN configuration:</span></span>
    - <span data-ttu-id="29581-118">Vytvářet nebo odebírat sítě VLAN</span><span class="sxs-lookup"><span data-stu-id="29581-118">Create or remove VLAN</span></span>
    - <span data-ttu-id="29581-119">Povolit nebo zakázat sítě VLAN</span><span class="sxs-lookup"><span data-stu-id="29581-119">Enable or disable VLAN</span></span>
    - <span data-ttu-id="29581-120">Zobrazení výčtu sítě VLAN</span><span class="sxs-lookup"><span data-stu-id="29581-120">Enumerate VLAN</span></span>
    - <span data-ttu-id="29581-121">Popisný název sady síť VLAN</span><span class="sxs-lookup"><span data-stu-id="29581-121">Set friendly name to a VLAN</span></span>

- <span data-ttu-id="29581-122">Konfigurace portu vrstvy 2:</span><span class="sxs-lookup"><span data-stu-id="29581-122">Layer 2 port configuration:</span></span>
    - <span data-ttu-id="29581-123">Zobrazení výčtu porty</span><span class="sxs-lookup"><span data-stu-id="29581-123">Enumerate ports</span></span>
    - <span data-ttu-id="29581-124">Povolit nebo zakázat porty</span><span class="sxs-lookup"><span data-stu-id="29581-124">Enable or disable ports</span></span>
    - <span data-ttu-id="29581-125">Režimy port sady a vlastnosti</span><span class="sxs-lookup"><span data-stu-id="29581-125">Set port modes and properties</span></span>
    - <span data-ttu-id="29581-126">Přidat nebo přidružit sítě VLAN Trunk nebo přístup na portu</span><span class="sxs-lookup"><span data-stu-id="29581-126">Add or associate VLAN to Trunk or Access on the port</span></span>

<span data-ttu-id="29581-127">Začněte se seznamovat se tak, že vyhledá všechny rutiny NetworkSwitch!</span><span class="sxs-lookup"><span data-stu-id="29581-127">Start exploring by looking for all of the NetworkSwitch cmdlets!</span></span>

```powershell
PS> Get-Command *-NetworkSwitch*

| CommandType | Name                                      | Source        |
|-------------|-------------------------------------------|---------------|
|             |                                           |               |
| Function    | Disable-NetworkSwitchEthernetPort         | NetworkSwitch |
| Function    | Disable-NetworkSwitchFeature              | NetworkSwitch |
| Function    | Disable-NetworkSwitchVlan                 | NetworkSwitch |
| Function    | Enable-NetworkSwitchEthernetPort          | NetworkSwitch |
| Function    | Enable-NetworkSwitchFeature               | NetworkSwitch |
| Function    | Enable-NetworkSwitchVlan                  | NetworkSwitch |
| Function    | Get-NetworkSwitchEthernetPort             | NetworkSwitch |
| Function    | Get-NetworkSwitchFeature                  | NetworkSwitch |
| Function    | Get-NetworkSwitchGlobalData               | NetworkSwitch |
| Function    | Get-NetworkSwitchVlan                     | NetworkSwitch |
| Function    | New-NetworkSwitchVlan                     | NetworkSwitch |
| Function    | Remove-NetworkSwitchEthernetPortIPAddress | NetworkSwitch |
| Function    | Remove-NetworkSwitchVlan                  | NetworkSwitch |
| Function    | Restore-NetworkSwitchConfiguration        | NetworkSwitch |
| Function    | Save-NetworkSwitchConfiguration           | NetworkSwitch |
| Function    | Set-NetworkSwitchEthernetPortIPAddress    | NetworkSwitch |
| Function    | Set-NetworkSwitchPortMode                 | NetworkSwitch |
| Function    | Set-NetworkSwitchPortProperty             | NetworkSwitch |
| Function    | Set-NetworkSwitchVlanProperty             | NetworkSwitch |
```

<span data-ttu-id="29581-128">Další informace najdete v Jana Snover WMF 5.0 Preview oznámení příspěvku na blogu: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx></span><span class="sxs-lookup"><span data-stu-id="29581-128">More information is available in Jeffrey Snover’s WMF 5.0 Preview announcement blog post: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx></span></span>