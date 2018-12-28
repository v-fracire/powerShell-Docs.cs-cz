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
# <a name="update-nodes-from-a-pull-server"></a>Aktualizovat uzly ze serveru vyžádané replikace

Následující části se předpokládá, že jste již nastavili serveru vyžádaných replikací s. Pokud jste nenastavili serveru o přijetí změn, můžete použít následující příručky:

- [Nastavení serveru vyžádané replikace DSC SMB](pullServerSmb.md)
- [Nastavení serveru vyžádané replikace DSC HTTP](pullServer.md)

Každý cílový uzel je nakonfigurovat ke stažení konfigurace, prostředků a dokonce i oznámit svůj stav. Tento článek vám ukáže jak nahrát prostředky, takže jsou k dispozici chcete stahovat a nastavte klienty, aby automaticky stáhnout prostředky. Když uzel obdrží přiřazených konfigurací prostřednictvím **o přijetí změn** nebo **Push** (v5), automaticky stáhne všechny prostředky, které konfigurace z umístění zadaného v LCM vyžaduje.

## <a name="using-the-update-dscconfiguration-cmdlet"></a>Pomocí rutiny Update-DSCConfiguration

V Powershellu 5.0 [Update-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/update-dscconfiguration) rutiny, vynutí uzel k aktualizaci konfigurace ze serveru vyžádaných gurovaný LCM.

```powershell
Update-DSCConfiguration -ComputerName "Server01"
```

## <a name="using-invoke-cimmethod"></a>Pomocí Invoke CIMMethod

V Powershellu 4.0, můžete ručně vynutit klienta o přijetí změn aktualizovat jeho konfiguraci pomocí [Invoke CIMMethod](/powershell/module/cimcmdlets/invoke-cimmethod). Následující příklad vytvoří relaci CIM pomocí zadaných přihlašovacích údajů, vyvolá vhodnou metodu CIM a odebere relace.

```powershell
$cimSession = New-CimSession -ComputerName "Server01" -Credential $(Get-Credential)
Invoke-CimMethod -CimSession $cimSession -Namespace 'root/microsoft/windows/desiredstateconfiguration' -Class 'MSFT_DscLocalConfigurationManager' -MethodName 'PerformRequiredConfigurationChecks' -Arguments @{ 'Flags' = [uint32]1 } -Verbose
$cimSession | Remove-CimSession
```

## <a name="see-also"></a>Viz také

[PerformRequiredConfigurationChecks](/powershell/dsc/msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks)
