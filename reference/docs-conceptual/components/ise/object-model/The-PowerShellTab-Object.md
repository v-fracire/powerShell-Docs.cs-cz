---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt PowerShellTab
ms.assetid: a9b58556-951b-4f48-b3ae-b351b7564360
ms.openlocfilehash: 577e2aaaddf3071801816d9ae91dbf0006dd5072
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403697"
---
# <a name="the-powershelltab-object"></a>Objekt PowerShellTab

**PowerShellTab** objekt představuje běhové prostředí Windows PowerShell.

## <a name="methods"></a>Metody

### <a name="invoke-script-"></a>Vyvolání\( skriptu \)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Spustí daný skript v kartě prostředí PowerShell.

> [!NOTE]
> Tato metoda funguje jenom na ostatních kartách Powershellu není PowerShell tab, ze kterého je spuštěn. Nevrátí se žádné objekt nebo hodnotu. Pokud kód změní jakákoli proměnná, tyto změny zachovat na kartě, proti kterému se vyvolala příkazu.

**Skript** -System.Management.Automation.ScriptBlock nebo řetězec bloku skriptu ke spuštění.

```powershell
# Manually create a second PowerShell tab before running this script.
# Return to the first PowerShell tab and type the following command
$psISE.PowerShellTabs[1].Invoke({dir})
```

### <a name="invokesynchronous-script-usenewscope-millisecondstimeout-"></a>InvokeSynchronous\( skriptu, \[useNewScope\], millisecondsTimeout \)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Spustí daný skript v kartě prostředí PowerShell.

> [!NOTE]
> Tato metoda funguje jenom na ostatních kartách Powershellu není PowerShell tab, ze kterého je spuštěn. Blok skriptu běží a libovolnou hodnotu, která je vrácena ze skriptu se vrátí do prostředí pro spuštění ze kterého můžete vyvolat příkaz. Pokud tohoto příkazu trvá delší dobu než **millesecondsTimeout** Určuje hodnotu, pak příkaz selže a dojde k výjimce: "Časový limit operace vypršel."

**Skript** -System.Management.Automation.ScriptBlock nebo řetězec bloku skriptu ke spuštění.

**\[useNewScope\]**  – volitelný logický, výchozí hodnota je **$true** -li nastavena na **$true**, pak se v rámci kterého chcete spustit příkaz vytvoří nový obor. Neprovede žádné změny běhové prostředí PowerShell tab, která je určená příkazu.

**\[millisecondsTimeout\]**  -volitelné celé číslo, která jako výchozí **500**.
Pokud příkaz nebyl dokončen v zadaném čase, pak tento příkaz vygeneruje **TimeoutException** se zprávou "operace vypršel."

```powershell
# Create a new PowerShell tab and then switch back to the first
$psISE.PowerShellTabs.Add()
$psISE.PowerShellTabs.SetSelectedPowerShellTab($psISE.PowerShellTabs[0])

# Invoke a simple command on the other tab, in its own scope
$psISE.PowerShellTabs[1].InvokeSynchronous('$x=1', $false)
# You can switch to the other tab and type '$x' to see that the value is saved there.

# This example sets a value in the other tab (in a different scope)
# and returns it through the pipeline to this tab to store in $a
$a = $psISE.PowerShellTabs[1].InvokeSynchronous('$z=3;$z')
$a

# This example runs a command that takes longer than the allowed timeout value
# and measures how long it runs so that you can see the impact
Measure-Command {$psISE.PowerShellTabs[1].InvokeSynchronous('sleep 10', $false, 5000)}
```

## <a name="properties"></a>Properties

### <a name="addonsmenu"></a>AddOnsMenu

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, která získá nabídce doplňky pro PowerShell tab.

```powershell
# Clear the Add-ons menu if one exists.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
# Create an AddOns menu with an accessor.
# Note the use of "_"  as opposed to the "&" for mapping to the fast key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add('_Process', {Get-Process}, 'Alt+P')
# Add a nested menu.
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add('Parent', $null, $null)
$parentAdded.SubMenus.Add('_Dir', {dir}, 'Alt+D')
# Show the Add-ons menu on the current PowerShell tab.
$psISE.CurrentPowerShellTab.AddOnsMenu
```

### <a name="caninvoke"></a>CanInvoke

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Jen pro čtení logická vlastnost, která vrací **$true** hodnotu, pokud skript lze vyvolat pomocí [Invoke (skript)](#invoke-script-) metody.

```powershell
# CanInvoke will be false if the PowerShell
# tab is running a script that takes a while, and you
# check its properties from another PowerShell tab. It is
# always false if checked on the current PowerShell tab.
# Manually create a second PowerShell tab before running this script.
# Return to the first tab and type
$secondTab = $psISE.PowerShellTabs[1]
$secondTab.CanInvoke
$secondTab.Invoke({sleep 20})
$secondTab.CanInvoke
```

### <a name="consolepane"></a>Consolepane

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.  V rozhraní Windows PowerShell ISE 2.0 to nazýval **CommandPane**.

Vlastnost jen pro čtení, který získá podokně konzoly [editor](The-ISEEditor-Object.md) objektu.

```powershell
# Gets the Console Pane editor.
$psISE.CurrentPowerShellTab.ConsolePane
```

### <a name="displayname"></a>DisplayName

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost pro čtení i zápis, která získá nebo nastaví text, který se zobrazí na kartě prostředí PowerShell. Ve výchozím nastavení, jsou karty s názvem "Powershellu #", kde znak # představuje číslo.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="expandedscript"></a>ExpandedScript

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Čtení a zápis logická vlastnost, která určuje, jestli je v podokně skriptu rozšířit nebo skrytý.

```powershell
# Toggle the expanded script property to see its effect.
$psISE.CurrentPowerShellTab.ExpandedScript = !$psISE.CurrentPowerShellTab.ExpandedScript
```

### <a name="files"></a>Soubory

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, který získá [kolekce souborů skriptu](The-ISEFileCollection-Object.md) , které jsou otevřeny v kartě prostředí PowerShell.

```powershell
$newFile = $psISE.CurrentPowerShellTab.Files.Add()
$newFile.Editor.Text = "a`r`nb"
# Gets the line count
$newFile.Editor.LineCount
```

### <a name="output"></a>Výstup

Tato funkce je k dispozici v rozhraní Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.  V novějších verzích Windows PowerShell ISE, můžete použít **ConsolePane** objekt pro stejné účely.

Vlastnost jen pro čtení, který získá podokno výstup aktuálního [editor](The-ISEEditor-Object.md).

```powershell
# Clears the text in the Output pane.
$psISE.CurrentPowerShellTab.output.clear()
```

### <a name="prompt"></a>Výzvu

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, která získá aktuální text výzvy. Poznámka: **výzvy** může být funkce přepsána uživatelem "™ s profilu. Pokud je výsledkem jiného než jednoduchým řetězcem, pak tato vlastnost nic nespouští.

```powershell
# Gets the current prompt text.
$psISE.CurrentPowerShellTab.Prompt
```

### <a name="showcommands"></a>ShowCommands

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Vlastnost pro čtení i zápis, která označuje, pokud je aktuálně zobrazí podokno příkazů.

```powershell
# Gets the current status of the Commands pane and stores it in the $a variable
$a = $psISE.CurrentPowerShellTab.ShowCommands
# if $a is $false, then turn the Commands pane on by changing the value to $true
if (!$a) {$psISE.CurrentPowerShellTab.ShowCommands = $true}
```

### <a name="statustext"></a>StatusText

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, který získá **PowerShellTab** textu stavu.

```powershell
# Gets the current status text,
$psISE.CurrentPowerShellTab.StatusText
```

### <a name="horizontaladdontoolspaneopened"></a>HorizontalAddOnToolsPaneOpened

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Vlastnost jen pro čtení určující, zda je vodorovné podokna nástrojů Doplňky aktuálně otevřené.

```powershell
# Gets the current state of the horizontal Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

### <a name="verticaladdontoolspaneopened"></a>VerticalAddOnToolsPaneOpened

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Vlastnost jen pro čtení, která označuje, zda je aktuálně otevřené svislé podokna nástrojů doplňky.

```powershell
# Turns on the Commands pane
$psISE.CurrentPowerShellTab.ShowCommands = $true
# Gets the current state of the vertical Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

## <a name="see-also"></a>Viz také

- [Objekt PowerShellTabCollection](The-PowerShellTabCollection-Object.md)
- [Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)