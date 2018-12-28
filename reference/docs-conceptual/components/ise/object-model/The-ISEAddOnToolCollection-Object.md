---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEAddOnToolCollection
ms.assetid: 634eab89-0845-4016-974b-361b09bb8f7b
ms.openlocfilehash: ff4f19d1a85a592f2f4f09c62caa0971751bdff7
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403870"
---
# <a name="the-iseaddontoolcollection-object"></a>Objekt ISEAddOnToolCollection

**ISEAddOnToolCollection** objektu je kolekce **ISEAddOnTool** objekty. Příkladem je **$psISE.CurrentPowerShellTab.VerticalAddOnTools** objektu.

## <a name="methods"></a>Metody

### <a name="add-name-controltype-isvisible-"></a>Přidat\( název, ControlType, \[IsVisible\] \)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Přidá nový nástroj doplněk do kolekce. Vrací doplněk nově přidaný nástroj. Před spuštěním tohoto příkazu, musíte nainstalovat doplněk nástroje v místním počítači a načtení sestavení.

**Název** -řetězec Určuje zobrazovaný název doplňku nástroj, který se přidá do prostředí PowerShell ISE Windows.

**ControlType** – Určuje typ ovládacího prvku, který je přidán.

**\[IsVisible\]**  – volitelný logický-li nastavena na **$true**, nástroj pro doplněk je okamžitě viditelné v podokně související nástroje.

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a>Odebrat\( položky \)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Odebere nástroj zadaný doplněk z kolekce.

**Položka** -Microsoft.PowerShell.Host.ISE.ISEAddOnTool určuje objekt, který má být odebrán z Windows PowerShell ISE.

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a>SetSelectedPowerShellTab\( psTab \)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Vybere prostředí PowerShell karty, která **psTab** parametrem.

**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab Powershellu kartu k výběru.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="remove-pstab-"></a>Odebrat\( psTab \)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Odebere prostředí PowerShell karty, která **psTab** parametrem.

**psTab** – karta Microsoft.PowerShell.Host.ISE.PowerShellTab Powershellu odebrat.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a>Viz také

- [Objekt PowerShellTab](The-PowerShellTab-Object.md)
- [Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)