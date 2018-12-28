---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt PowerShellTabCollection
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: d9088b26de35360b8258d3f15924b3010a986d15
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403874"
---
# <a name="the-powershelltabcollection-object"></a>Objekt PowerShellTabCollection

**PowerShellTab** objektu kolekce je kolekce **PowerShellTab** objekty. Každý **PowerShellTab** objekt funguje jako samostatné běhové prostředí. Je instancí třídy Microsoft.PowerShell.Host.ISE.PowerShellTabs. Příkladem je **$psISE.PowerShellTabs** objektu.

## <a name="methods"></a>Metody

### <a name="add"></a>Přidat\(\)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Na nové kartě Powershellu přidá do kolekce. Vrátí nově přidanou kartu.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a>Odebrat\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Odebere kartu, která je zadána **psTab** parametru.

**psTab** karty Powershellu k odebrání.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a>SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vybere PowerShell tab, která je zadána **psTab** k němu na aktivní kartě prostředí PowerShell parametr.

**psTab** Powershellu kartu k výběru.

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
- [Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)