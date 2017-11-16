---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt ISEMenuItem
ms.assetid: a16660bd-0aee-46fd-ac17-3f022165d089
ms.openlocfilehash: 5561955040e56110a6af0619c286548f5812fb47
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="the-isemenuitem-object"></a>Objekt ISEMenuItem
  **ISEMenuItem** objekt je instance třídy Microsoft.PowerShell.Host.ISE.ISEMenuItem. Všechny objekty nabídky na **doplňky** nabídky jsou instancemi třídy **Microsoft.PowerShell.Host.ISE.ISEMenuItem** třídy.

## <a name="properties"></a>Properties

### <a name="displayname"></a>DisplayName
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, získá zobrazovaný název položky nabídky.

```
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName

```

### <a name="action"></a>Akce
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, získá blok skriptu. Po kliknutí na položku nabídky vyvolá akci.

```
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item 
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

### <a name="shortcut"></a>Zástupce
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, který získá Windows zadejte klávesové zkratky pro položku nabídky.

```
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

### <a name="submenus"></a>Dílčích
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, který získá [seznam dílčích](The-ISEMenuItemCollection-Object.md) položky nabídky.

```
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a>Příklad skriptování
 Abyste lépe pochopili, použití v nabídce doplňky a jeho Skriptovatelná vlastnosti, přečíst v následujícím příkladu skriptování.

```

# This is a scripting example that shows the use of the Add-ons menu.
# Clear the Add-ons menu if any entries currently exist
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()

# Add an Add-ons menu item with an shortcut and fast access key.
# Note the use of “_”  as opposed to the “&” for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P") 
# Add a nested menu - a parent and a child submenu item. 
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("Parent",$null,$null) 
$parentAdded.SubMenus.Add("_Dir",{dir},"Alt+D")

```

## <a name="see-also"></a>Viz také
- [Objekt ISEMenuItemCollection](The-ISEMenuItemCollection-Object.md) 
- [ISE Windows PowerShell skriptování objektový Model](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Odkaz na objekt modelu Windows PowerShell ISE](Windows-PowerShell-ISE-Object-Model-Reference.md)
- [Hierarchie ISE objektů modelu](The-ISE-Object-Model-Hierarchy.md)
