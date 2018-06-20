---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEMenuItemCollection
ms.assetid: 0c0f5484-3320-408e-8534-5bd1c8e48512
ms.openlocfilehash: 7e5030416df394aaa9e9d3f63978e204a7faabf1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954700"
---
# <a name="the-isemenuitemcollection-object"></a>Objekt ISEMenuItemCollection

**ISEMenuItemCollection** objektu je kolekce **ISEMenuItem** objekty. Je instance třídy Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection. Příkladem je **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** objekt, který slouží k přizpůsobení **rozšíření** nabídky v systému Windows PowerShell® Integrované skriptovací prostředí (ISE).

## <a name="method"></a>Metoda

### <a name="addstring-displayname-systemmanagementautomationscriptblock-action-systemwindowsinputkeygesture-shortcut-"></a>Přidat\(řetězec zástupce System.Windows.Input.KeyGesture DisplayName, System.Management.Automation.ScriptBlock akce \)

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Přidá položku nabídky do kolekce.

**DisplayName** zobrazovaný název v nabídce Přidat.

**Akce** **System.Management.Automation.ScriptBlock** objekt, který určuje akci, která je pro tuto položku nabídky.

**Zástupce** klávesové zkratky pro akci.

**Vrátí** The ISEMenuItem objekt, který byl právě přidali.

```powershell
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
```

### <a name="clear"></a>Zrušte zaškrtnutí\(\)

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Odebere všechny dílčích z položky nabídky.

```powershell
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
```

## <a name="see-also"></a>Viz také

- [Objekt ISEMenuItem](The-ISEMenuItem-Object.md)
- [Účelem ISE Windows PowerShell skriptování objektový Model](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)