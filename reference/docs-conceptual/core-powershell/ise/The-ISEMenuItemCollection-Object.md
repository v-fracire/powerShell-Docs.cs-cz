---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt ISEMenuItemCollection
ms.assetid: 0c0f5484-3320-408e-8534-5bd1c8e48512
ms.openlocfilehash: 7ce9132021d4d5e755503e0adb355beb388a625a
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="the-isemenuitemcollection-object"></a>Objekt ISEMenuItemCollection
  **ISEMenuItemCollection** objektu je kolekce **ISEMenuItem** objekty. Je instance třídy Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection. Příkladem je **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** objekt, který slouží k přizpůsobení **rozšíření** nabídky v systému Windows PowerShell® Integrované skriptovací prostředí (ISE).

## <a name="method"></a>Metoda

### <a name="addstring-displayname-systemmanagementautomationscriptblock-action-systemwindowsinputkeygesture-shortcut-"></a>Přidat\(řetězec zástupce System.Windows.Input.KeyGesture DisplayName, System.Management.Automation.ScriptBlock akce\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Přidá položku nabídky do kolekce.

 **DisplayName** zobrazovaný název v nabídce Přidat.

 **Akce** **System.Management.Automation.ScriptBlock** objekt, který určuje akci, která je pro tuto položku nabídky.

 **Zástupce** klávesové zkratky pro akci.

 **Vrátí** The ISEMenuItem objekt, který byl právě přidali.

```
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
```

### <a name="clear"></a>Zrušte zaškrtnutí\(\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Odebere všechny dílčích z položky nabídky.

```
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

```

## <a name="see-also"></a>Viz také
- [Objekt ISEMenuItem](The-ISEMenuItem-Object.md) 
- [ISE Windows PowerShell skriptování objektový Model](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Odkaz na objekt modelu Windows PowerShell ISE](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [Hierarchie ISE objektů modelu](The-ISE-Object-Model-Hierarchy.md)

  
