---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt PowerShellTabCollection
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: dcdc16ae126453b6ade64917ac4950cc05e5f8ad
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="the-powershelltabcollection-object"></a>Objekt PowerShellTabCollection
  **PowerShellTab** objektu kolekce je kolekce **PowerShellTab** objekty. Každý **PowerShellTab** objekt funguje jako samostatné běhového prostředí. Je instance třídy Microsoft.PowerShell.Host.ISE.PowerShellTabs. Příkladem je **$psISE.PowerShellTabs** objektu.

## <a name="methods"></a>Metody

### <a name="add"></a>Přidat\(\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Přidá novou kartu prostředí PowerShell do kolekce. Vrátí kartě nově přidaný.

```
$NewTab=$psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab"
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a>Odebrat\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Odebere kartu, která je zadána **psTab** parametr.

 **psTab** karty prostředí PowerShell k odebrání.

```

$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="This tab will go away in 5 seconds" 
sleep 5 
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a>SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vybere kartě prostředí PowerShell, která je zadána **psTab** parametr aby kartě aktuálně aktivní prostředí PowerShell.

 **psTab** karty prostředí PowerShell k výběru.

```
# Save the current tab in a variable and rename it
$OldTab = $psISE.CurrentPowerShellTab
$psISE.CurrentPowerShellTab.DisplayName="Old Tab"
# Create a new tab and give it a new display name
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab" 
# Switch back to the original tab
$psISE.PowerShellTabs.SelectedPowerShellTab=$oldtab
```

## <a name="see-also"></a>Viz také
- [Objekt PowerShellTab](The-PowerShellTab-Object.md) 
- [ISE Windows PowerShell skriptování objektový Model](../ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Odkaz na objekt modelu Windows PowerShell ISE](../ise/Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [Hierarchie ISE objektů modelu](../ise/The-ISE-Object-Model-Hierarchy.md)

  
