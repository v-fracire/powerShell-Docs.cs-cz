---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEMenuItemCollection
ms.assetid: 0c0f5484-3320-408e-8534-5bd1c8e48512
ms.openlocfilehash: 7e5030416df394aaa9e9d3f63978e204a7faabf1
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403877"
---
# <a name="the-isemenuitemcollection-object"></a>Objekt ISEMenuItemCollection

**ISEMenuItemCollection** objektu je kolekce **ISEMenuItem** objekty. Je instancí třídy Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection. Příkladem je **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** objekt, který se používá k úpravě **doplněk** nabídky ve Windows Powershellu® integrovaném skriptovacím prostředí (ISE).

## <a name="method"></a>Metoda

### <a name="addstring-displayname-systemmanagementautomationscriptblock-action-systemwindowsinputkeygesture-shortcut-"></a>Přidat\(řetězec DisplayName, akce System.Management.Automation.ScriptBlock System.Windows.Input.KeyGesture zástupce \)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Přidá položku nabídky do kolekce.

**DisplayName** zobrazovaný název nabídky, které mají být přidány.

**Akce** **System.Management.Automation.ScriptBlock** objekt, který určuje akci, která souvisí s touto položkou nabídky.

**Místní** klávesové zkratky pro akci.

**Vrátí** The ISEMenuItem objekt, který byl právě přidali.

```powershell
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
```

### <a name="clear"></a>Vymazat\(\)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Odebere všechny podnabídek z položky nabídky.

```powershell
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
```

## <a name="see-also"></a>Viz také

- [Objekt ISEMenuItem](The-ISEMenuItem-Object.md)
- [Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)