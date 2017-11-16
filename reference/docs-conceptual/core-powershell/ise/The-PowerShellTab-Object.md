---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt PowerShellTab
ms.assetid: a9b58556-951b-4f48-b3ae-b351b7564360
ms.openlocfilehash: 15d9a7474e4c2cf2a9ff8edb88802106489cdba1
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="the-powershelltab-object"></a>Objekt PowerShellTab
  **PowerShellTab** objekt představuje běhového prostředí Windows PowerShell.

## <a name="methods"></a>Metody

### <a name="invoke-script-"></a>Vyvolání\( skriptu\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Spustí daný skript na kartě prostředí PowerShell.

> [!NOTE]
> Tato metoda funguje jenom na ostatní karty prostředí PowerShell není na kartě prostředí PowerShell, ze kterého je spuštěno. Nevrací se žádné objekt nebo hodnota. Pokud kód upraví všechny proměnné, tyto změny uchová na kartě, pro kterou byl vyvolán příkaz.

 **Skript** -System.Management.Automation.ScriptBlock nebo řetězec bloku skriptu ke spuštění.

```
# Manually create a second PowerShell tab before running this script.
# Return to the first PowerShell tab and type the following command
$psise.PowerShellTabs[1].Invoke({dir})
```

### <a name="invokesynchronous-script-usenewscope-millisecondstimeout-"></a>InvokeSynchronous\( skriptu \[useNewScope\], millisecondsTimeout\)
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích. 

 Spustí daný skript na kartě prostředí PowerShell.

> [!NOTE]
> Tato metoda funguje jenom na ostatní karty prostředí PowerShell není na kartě prostředí PowerShell, ze kterého je spuštěno. Je-li spustit blok skriptu a jakoukoli hodnotu, která je vrácena z skript je vrácen do běhu prostředí, ze kterého můžete vyvolat příkaz. Pokud příkaz trvat delší dobu než **millesecondsTimeout** hodnota určuje, a potom příkaz selže a dojde k výjimce: "časový limit operace vypršel."

 **Skript** -System.Management.Automation.ScriptBlock nebo řetězec bloku skriptu ke spuštění.

 **\[useNewScope\]**  -volitelné logická hodnota, použije se výchozí hodnota **$true** Pokud nastavena na **$true**, pak se vytvoří nový obor v rámci kterého ke spuštění příkazu. Běhové prostředí na kartě prostředí PowerShell, který je zadán příkaz nemění.

 **\[millisecondsTimeout\]**  -volitelné celé číslo, které použije se výchozí hodnota **500**.
Pokud příkaz nebyl dokončen v určeném čase a potom příkaz generuje **TimeoutException** se zprávou "operace vypršel."

```
# create a new PowerShell tab and then switch back to the first
$PSise.PowerShellTabs.Add()
$psISE.PowerShellTabs.SetSelectedPowerShellTab($psISE.PowerShellTabs[0]) 

# Invoke a simple command on the other tab, in its own scope
$psISE.PowerShellTabs[1].InvokeSynchronous('$x=1',$false)
# You can switch to the other tab and type 'œ$x' to see that the value is saved there.

# This example sets a value in the other tab (in a different scope) 
# and returns it through the pipeline to this tab to store in $a
$a=$psISE.PowerShellTabs[1].InvokeSynchronous('$z=3;$z') 
$a

# This example runs a command that takes longer than the allowed timeout value
# and measures how long it runs so that you can see the impact
measure-command {$psISE.PowerShellTabs[1].InvokeSynchronous("sleep 10",$false,5000)}

```

## <a name="properties"></a>Properties

### <a name="addonsmenu"></a>AddOnsMenu
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, získá nabídce doplňky pro kartě prostředí PowerShell.

```
# Clear the Add-ons menu if one exists.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
# Create an AddOns menu with an accessor.
# Note the use of "_"  as opposed to the "&" for mapping to the fast key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P") 
# Add a nested menu. 
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("Parent",$null,$null) 
$parentAdded.SubMenus.Add("_Dir",{dir},"Alt+D")
# Show the Add-ons menu on the current PowerShell tab.
$psISE.CurrentPowerShellTab.AddOnsMenu
```

### <a name="caninvoke"></a>CanInvoke
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Jen pro čtení logická hodnota vlastnosti, která vrací **$true** hodnotu, pokud nelze vyvolat skript s [Invoke (skript)](#invoke-script-) metoda.

```
# CanInvoke will be false if the PowerShell
# tab is running a script that takes a while, and you
# check its properties from another PowerShell tab. It is
# always false if checked on the current PowerShell tab. 
# Manually create a second PowerShell tab before running this script.
# Return to the first tab and type
$secondTab = $psise.PowerShellTabs[1] 
$secondTab.CanInvoke 
$secondTab.Invoke({sleep 20})
$secondTab.CanInvoke

```

### <a name="consolepane"></a>Consolepane
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.  V prostředí Windows PowerShell ISE 2.0 to nazýval **CommandPane**.

 Vlastnost jen pro čtení, který získá podokně konzoly [editor](../ise/The-ISEEditor-Object.md) objektu.

```
# Gets the Console Pane editor.
$psISE.CurrentPowerShellTab.ConsolePane

```

### <a name="displayname"></a>DisplayName
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost pro čtení a zápis, který získá nebo nastaví text, který se zobrazí na kartě prostředí PowerShell. Ve výchozím nastavení, jsou karty s názvem "PowerShell #", kde znak # představuje číslo.

```
$newTab = $psise.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="Brand New Tab"
```

### <a name="expandedscript"></a>ExpandedScript
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Pro čtení a zápis vlastnost typu Boolean, která určuje, zda je v podokně skriptu rozšířit nebo skrytý.

```
# Toggle the expanded script property to see its effect.
$PSise.CurrentPowerShellTab.ExpandedScript=!$PSise.CurrentPowerShellTab.ExpandedScript

```

### <a name="files"></a>Soubory
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, který získá [kolekce souborů skriptů](../ise/The-ISEFileCollection-Object.md) , jsou otevřeny v kartě prostředí PowerShell.

```
$newFile = $psISE.CurrentPowerShellTab.Files.Add()
$newFile.Editor.Text = "a`r`nb" 
# Gets the line count
$newFile.Editor.LineCount
```

### <a name="output"></a>Výstup
  Tato funkce je k dispozici v prostředí Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.  V novějších verzích systému Windows PowerShell ISE, můžete použít **ConsolePane** objekt pro stejné účely.

 Vlastnost jen pro čtení, který získá podokno výstup aktuálního [editor](../ise/The-ISEEditor-Object.md).

```
# Clears the text in the Output pane.
$psise.CurrentPowerShellTab.output.clear()
```

### <a name="prompt"></a>řádku
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, získá aktuální text výzvy. Poznámka: **výzva** funkce mohou být přepsány uživatele '™ s profil. Pokud je výsledek než jednoduchý řetězec, pak tato vlastnost vrátí nic.

```
# Gets the current prompt text.
$psISE.CurrentPowerShellTab.Prompt
```

### <a name="showcommands"></a>ShowCommands
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích. 

 Vlastnost pro čtení a zápis, která označuje, pokud je aktuálně zobrazený na panelu příkazů.

```
# Gets the current status of the Commands pane and stores it in the $a variable
$a = $psISE.CurrentPowerShellTab.ShowCommands
# if $a is $false, then turn the Commands pane on by changing the value to $True
if (!$a) {$psISE.CurrentPowerShellTab.ShowCommands=$True}
```

### <a name="statustext"></a>StatusText
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, který získá **PowerShellTab** stav text.

```
# Gets the current status text,
$psISE.CurrentPowerShellTab.StatusText
```

### <a name="horizontaladdontoolspaneopened"></a>HorizontalAddOnToolsPaneOpened
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích. 

 Vlastnost jen pro čtení, která určuje, zda je aktuálně otevřených podokna nástrojů horizontální rozšíření.

```
# Gets the current state of the horizontal Add-ons tool pane. 
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

### <a name="verticaladdontoolspaneopened"></a>VerticalAddOnToolsPaneOpened
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích. 

 Vlastnost jen pro čtení, která určuje, zda je aktuálně otevřených podokna nástrojů svislé rozšíření.

```
# Turns on the Commands pane
$psISE.CurrentPowerShellTab.ShowCommands=$True
# Gets the current state of the vertical Add-ons tool pane. 
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

## <a name="see-also"></a>Viz také
- [Objekt PowerShellTabCollection](The-PowerShellTabCollection-Object.md) 
- [ISE Windows PowerShell skriptování objektový Model](../ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Odkaz na objekt modelu Windows PowerShell ISE](../ise/Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [Hierarchie ISE objektů modelu](../ise/The-ISE-Object-Model-Hierarchy.md)

  
