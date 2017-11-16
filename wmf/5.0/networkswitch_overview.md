---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 80852bf750700d549de24e150ffd89ac55b7bf88
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="network-switch-management-with-powershell"></a>Správa přepínače sítě pomocí prostředí PowerShell

**Get-NetworkSwitchEthernetPort** rutina nyní vrátí následující doplňkové informace s instancemi:

- IP adresa – IP adresa přidružená port
- PortMode – režim portu: přístup, postup nebo trunk
- AccessVLAN – ID sítě VLAN přidružené tento port v přístupovém režimu
- TrunkedVLANList – seznam ID sítě VLAN přiřazený k tomuto portu v páteřním režimu

## <a name="fundamental-network-switch-management-with-windows-powershell"></a>Správa přepínač základní sítě pomocí prostředí Windows PowerShell

Rutiny síťového přepínače, ve WMF 5.0, umožňují použít přepínač virtuální sítě LAN (VLAN) a základní konfigurací portu síťového přepínače vrstvy 2 na Windows Server 2012 R2 logo certified síťové přepínače. Microsoft stále snaží podpora [Datacenter Abstraction](http://technet.microsoft.com/en-us/cloud/dal.aspx) vize Layer (DAL) a zobrazit hodnotu pro naše zákazníky a partnery v tomto prostor. Pomocí těchto rutin můžete provést:

- Globální přepínači konfigurace, jako například:
    - Název hostitele sady
    - Hlavička set přepínače
    - Trvalá konfigurace
    - Povolení nebo zakázání funkce

- Konfigurace sítě VLAN:
    - Vytvářet nebo odebírat sítě VLAN
    - Povolit nebo zakázat sítě VLAN
    - Zobrazení výčtu sítě VLAN
    - Popisný název sady síť VLAN

- Konfigurace portu vrstvy 2:
    - Zobrazení výčtu porty
    - Povolit nebo zakázat porty
    - Režimy port sady a vlastnosti
    - Přidat nebo přidružit sítě VLAN Trunk nebo přístup na portu

Začněte se seznamovat se tak, že vyhledá všechny rutiny NetworkSwitch!

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

Další informace najdete v Jana Snover WMF 5.0 Preview oznámení příspěvku na blogu: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx>

