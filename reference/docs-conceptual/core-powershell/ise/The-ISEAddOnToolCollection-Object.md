---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEAddOnToolCollection
ms.assetid: 634eab89-0845-4016-974b-361b09bb8f7b
ms.openlocfilehash: ff4f19d1a85a592f2f4f09c62caa0971751bdff7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="the-iseaddontoolcollection-object"></a>Objekt ISEAddOnToolCollection

**ISEAddOnToolCollection** objektu je kolekce **ISEAddOnTool** objekty. Příkladem je **$psISE.CurrentPowerShellTab.VerticalAddOnTools** objektu.

## <a name="methods"></a>Metody

### <a name="add-name-controltype-isvisible-"></a>Přidat\( název, ControlType, \[IsVisible\] \)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

Přidá nový nástroj rozšíření do kolekce. Vrátí nástroj nově přidaného rozšíření. Než spustíte tento příkaz, musíte nainstalovat nástroje rozšíření v místním počítači a načtení sestavení.

**Název** -řetězec Určuje zobrazovaný název rozšíření nástroj, který je přidán do systému Windows PowerShell ISE.

**ControlType** – typ určuje ovládací prvek, který je přidán.

**\[IsVisible –\]**  -volitelné Boolean Pokud nastavit **$true**, nástroj rozšíření je okamžitě viditelné v podokně související nástroje.

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a>Odebrat\( položky \)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

Odebere zadané rozšíření nástroj z kolekce.

**Položka** -Microsoft.PowerShell.Host.ISE.ISEAddOnTool určuje objekt, který má být odebrán ze systému Windows PowerShell ISE.

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a>SetSelectedPowerShellTab\( psTab \)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

Vybere PowerShell kartě **psTab** parametrem.

**psTab** – karta Microsoft.PowerShell.Host.ISE.PowerShellTab prostředí PowerShell k výběru.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="remove-pstab-"></a>Odebrat\( psTab \)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

Odebere PowerShell kartě **psTab** parametrem.

**psTab** – karta Microsoft.PowerShell.Host.ISE.PowerShellTab prostředí PowerShell k odebrání.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a>Viz také

- [Objekt PowerShellTab](The-PowerShellTab-Object.md)
- [Účelem ISE Windows PowerShell skriptování objektový Model](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)