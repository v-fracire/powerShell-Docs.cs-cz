---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 11b5e36f703c242e0bc820ab19d11d39305fa90c
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="network-switch-management-with-powershell"></a>Použití PowerShellu ke správě síťového přepínače

**Get-NetworkSwitchEthernetPort** rutina nyní vrátí následující doplňkové informace s instancemi:

- IP adresa – IP adresa přidružená port
- PortMode – režim portu: přístup, postup nebo trunk
- AccessVLAN – ID sítě VLAN přidružené tento port v přístupovém režimu
- TrunkedVLANList – seznam ID sítě VLAN přiřazený k tomuto portu v páteřním režimu

## <a name="fundamental-network-switch-management-with-windows-powershell"></a>Správa přepínač základní sítě pomocí prostředí Windows PowerShell

Rutiny síťového přepínače, ve WMF 5.0, umožňují použít přepínač virtuální sítě LAN (VLAN) a základní konfigurací portu síťového přepínače vrstvy 2 na Windows Server 2012 R2 logo certified síťové přepínače. Microsoft stále snaží podpora [Datacenter Abstraction](http://technet.microsoft.com/cloud/dal.aspx) vize Layer (DAL) a zobrazit hodnotu pro naše zákazníky a partnery v tomto prostor. Pomocí těchto rutin můžete provést:

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
