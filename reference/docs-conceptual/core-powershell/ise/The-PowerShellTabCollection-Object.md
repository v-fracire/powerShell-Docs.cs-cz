---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt PowerShellTabCollection
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: d9088b26de35360b8258d3f15924b3010a986d15
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953068"
---
# <a name="the-powershelltabcollection-object"></a>Objekt PowerShellTabCollection

**PowerShellTab** objektu kolekce je kolekce **PowerShellTab** objekty. Každý **PowerShellTab** objekt funguje jako samostatné běhového prostředí. Je instance třídy Microsoft.PowerShell.Host.ISE.PowerShellTabs. Příkladem je **$psISE.PowerShellTabs** objektu.

## <a name="methods"></a>Metody

### <a name="add"></a>Přidat\(\)

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Přidá novou kartu prostředí PowerShell do kolekce. Vrátí kartě nově přidaný.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a>Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Odebere kartu, která je zadána **psTab** parametr.

**psTab** karty prostředí PowerShell k odebrání.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a>SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vybere kartě prostředí PowerShell, která je zadána **psTab** parametr aby kartě aktuálně aktivní prostředí PowerShell.

**psTab** karty prostředí PowerShell k výběru.

```powershell
# Save the current tab in a variable and rename it
$oldTab = $psISE.CurrentPowerShellTab
$psISE.CurrentPowerShellTab.DisplayName = 'Old Tab'
# Create a new tab and give it a new display name
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
# Switch back to the original tab
$psISE.PowerShellTabs.SelectedPowerShellTab = $oldTab
```

## <a name="see-also"></a>Viz také

- [Objekt PowerShellTab](The-PowerShellTab-Object.md)
- [Účelem ISE Windows PowerShell skriptování objektový Model](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)