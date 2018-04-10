---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEMenuItem
ms.assetid: a16660bd-0aee-46fd-ac17-3f022165d089
ms.openlocfilehash: 556f88117c07100b1734c8ffd8956dce6efe6fb1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="the-isemenuitem-object"></a>Objekt ISEMenuItem

**ISEMenuItem** objekt je instance třídy Microsoft.PowerShell.Host.ISE.ISEMenuItem. Všechny objekty nabídky na **doplňky** nabídky jsou instancemi třídy **Microsoft.PowerShell.Host.ISE.ISEMenuItem** třídy.

## <a name="properties"></a>Properties

### <a name="displayname"></a>DisplayName

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnost jen pro čtení, získá zobrazovaný název položky nabídky.

```powershell
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName
```

### <a name="action"></a>Akce

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnost jen pro čtení, získá blok skriptu. Po kliknutí na položku nabídky vyvolá akci.

```powershell
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

### <a name="shortcut"></a>Zástupce

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnost jen pro čtení, který získá Windows zadejte klávesové zkratky pro položku nabídky.

```powershell
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

### <a name="submenus"></a>Dílčích

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnost jen pro čtení, který získá [seznam dílčích](The-ISEMenuItemCollection-Object.md) položky nabídky.

```powershell
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a>Příklad skriptování

Abyste lépe pochopili, použití v nabídce doplňky a jeho Skriptovatelná vlastnosti, přečíst v následujícím příkladu skriptování.

```powershell
# This is a scripting example that shows the use of the Add-ons menu.
# Clear the Add-ons menu if any entries currently exist
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

# Add an Add-ons menu item with an shortcut and fast access key.
# Note the use of “_”  as opposed to the “&” for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add('_Process', {Get-Process}, 'Alt+P')
# Add a nested menu - a parent and a child submenu item.
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('Parent', $null, $null)
$parentAdded.SubMenus.Add('_Dir', {dir}, 'Alt+D')
```

## <a name="see-also"></a>Viz také

- [Objekt ISEMenuItemCollection](The-ISEMenuItemCollection-Object.md)
- [Účelem ISE Windows PowerShell skriptování objektový Model](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)