---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt PowerShellTab
ms.assetid: a9b58556-951b-4f48-b3ae-b351b7564360
ms.openlocfilehash: c10f9106e31bb05828f1e76554ebe40ddb778340
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="the-powershelltab-object"></a><span data-ttu-id="f2711-103">Objekt PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="f2711-103">The PowerShellTab Object</span></span>

<span data-ttu-id="f2711-104">**PowerShellTab** objekt představuje běhového prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2711-104">The **PowerShellTab** object represents a Windows PowerShell runtime environment.</span></span>

## <a name="methods"></a><span data-ttu-id="f2711-105">Metody</span><span class="sxs-lookup"><span data-stu-id="f2711-105">Methods</span></span>

### <a name="invoke-script-"></a><span data-ttu-id="f2711-106">Vyvolání\( skriptu \)</span><span class="sxs-lookup"><span data-stu-id="f2711-106">Invoke\( Script \)</span></span>

<span data-ttu-id="f2711-107">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="f2711-107">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="f2711-108">Spustí daný skript na kartě prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2711-108">Runs the given script in the PowerShell tab.</span></span>

> [!NOTE]
> <span data-ttu-id="f2711-109">Tato metoda funguje jenom na ostatní karty prostředí PowerShell není na kartě prostředí PowerShell, ze kterého je spuštěno.</span><span class="sxs-lookup"><span data-stu-id="f2711-109">This method only works on other PowerShell tabs, not the PowerShell tab from which it is run.</span></span> <span data-ttu-id="f2711-110">Nevrací se žádné objekt nebo hodnota.</span><span class="sxs-lookup"><span data-stu-id="f2711-110">It does not return any object or value.</span></span> <span data-ttu-id="f2711-111">Pokud kód upraví všechny proměnné, tyto změny uchová na kartě, pro kterou byl vyvolán příkaz.</span><span class="sxs-lookup"><span data-stu-id="f2711-111">If the code modifies any variable, then those changes persist on the tab against which the command was invoked.</span></span>

<span data-ttu-id="f2711-112">**Skript** -System.Management.Automation.ScriptBlock nebo řetězec bloku skriptu ke spuštění.</span><span class="sxs-lookup"><span data-stu-id="f2711-112">**Script** - System.Management.Automation.ScriptBlock or String The script block to run.</span></span>

```powershell
# Manually create a second PowerShell tab before running this script.
# Return to the first PowerShell tab and type the following command
$psISE.PowerShellTabs[1].Invoke({dir})
```

### <a name="invokesynchronous-script-usenewscope-millisecondstimeout-"></a><span data-ttu-id="f2711-113">InvokeSynchronous\( skriptu \[useNewScope\], millisecondsTimeout \)</span><span class="sxs-lookup"><span data-stu-id="f2711-113">InvokeSynchronous\( Script, \[useNewScope\], millisecondsTimeout \)</span></span>

<span data-ttu-id="f2711-114">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="f2711-114">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="f2711-115">Spustí daný skript na kartě prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2711-115">Runs the given script in the PowerShell tab.</span></span>

> [!NOTE]
> <span data-ttu-id="f2711-116">Tato metoda funguje jenom na ostatní karty prostředí PowerShell není na kartě prostředí PowerShell, ze kterého je spuštěno.</span><span class="sxs-lookup"><span data-stu-id="f2711-116">This method only works on other PowerShell tabs, not the PowerShell tab from which it is run.</span></span> <span data-ttu-id="f2711-117">Je-li spustit blok skriptu a jakoukoli hodnotu, která je vrácena z skript je vrácen do běhu prostředí, ze kterého můžete vyvolat příkaz.</span><span class="sxs-lookup"><span data-stu-id="f2711-117">The script block is run and any value that is returned from the script is returned to the run environment from which you invoked the command.</span></span> <span data-ttu-id="f2711-118">Pokud příkaz trvat delší dobu než **millesecondsTimeout** hodnota určuje, a potom příkaz selže a dojde k výjimce: "časový limit operace vypršel."</span><span class="sxs-lookup"><span data-stu-id="f2711-118">If the command takes longer to run than the **millesecondsTimeout** value specifies, then the command fails with an exception: "The operation has timed out."</span></span>

<span data-ttu-id="f2711-119">**Skript** -System.Management.Automation.ScriptBlock nebo řetězec bloku skriptu ke spuštění.</span><span class="sxs-lookup"><span data-stu-id="f2711-119">**Script** - System.Management.Automation.ScriptBlock or String The script block to run.</span></span>

<span data-ttu-id="f2711-120">**\[useNewScope\]**  -volitelné logická hodnota, použije se výchozí hodnota **$true** Pokud nastavena na **$true**, pak se vytvoří nový obor v rámci kterého ke spuštění příkazu.</span><span class="sxs-lookup"><span data-stu-id="f2711-120">**\[useNewScope\]** -  Optional Boolean that defaults to **$true** If set to **$true**, then a new scope is created within which to run the command.</span></span> <span data-ttu-id="f2711-121">Běhové prostředí na kartě prostředí PowerShell, který je zadán příkaz nemění.</span><span class="sxs-lookup"><span data-stu-id="f2711-121">It does not modify the runtime environment of the PowerShell tab that is specified by the command.</span></span>

<span data-ttu-id="f2711-122">**\[millisecondsTimeout\]**  -volitelné celé číslo, které použije se výchozí hodnota **500**.</span><span class="sxs-lookup"><span data-stu-id="f2711-122">**\[millisecondsTimeout\]** -  Optional integer that defaults to **500**.</span></span>
<span data-ttu-id="f2711-123">Pokud příkaz nebyl dokončen v určeném čase a potom příkaz generuje **TimeoutException** se zprávou "operace vypršel."</span><span class="sxs-lookup"><span data-stu-id="f2711-123">If the command does not finish within the specified time, then the command generates a **TimeoutException** with the message "The operation has timed out."</span></span>

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

## <a name="properties"></a><span data-ttu-id="f2711-124">Properties</span><span class="sxs-lookup"><span data-stu-id="f2711-124">Properties</span></span>

### <a name="addonsmenu"></a><span data-ttu-id="f2711-125">AddOnsMenu</span><span class="sxs-lookup"><span data-stu-id="f2711-125">AddOnsMenu</span></span>

<span data-ttu-id="f2711-126">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="f2711-126">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="f2711-127">Vlastnost jen pro čtení, získá nabídce doplňky pro kartě prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2711-127">The read-only property that gets the Add-ons menu for the PowerShell tab.</span></span>

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

### <a name="caninvoke"></a><span data-ttu-id="f2711-128">CanInvoke</span><span class="sxs-lookup"><span data-stu-id="f2711-128">CanInvoke</span></span>

<span data-ttu-id="f2711-129">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="f2711-129">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="f2711-130">Jen pro čtení logická hodnota vlastnosti, která vrací **$true** hodnotu, pokud nelze vyvolat skript s [Invoke (skript)](#invoke-script-) metoda.</span><span class="sxs-lookup"><span data-stu-id="f2711-130">The read-only Boolean property that returns a **$true** value if a script can be invoked with the [Invoke( Script )](#invoke-script-) method.</span></span>

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

### <a name="consolepane"></a><span data-ttu-id="f2711-131">Consolepane</span><span class="sxs-lookup"><span data-stu-id="f2711-131">Consolepane</span></span>

<span data-ttu-id="f2711-132">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="f2711-132">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>  <span data-ttu-id="f2711-133">V prostředí Windows PowerShell ISE 2.0 to nazýval **CommandPane**.</span><span class="sxs-lookup"><span data-stu-id="f2711-133">In Windows PowerShell ISE 2.0 this was named **CommandPane**.</span></span>

<span data-ttu-id="f2711-134">Vlastnost jen pro čtení, který získá podokně konzoly [editor](../ise/The-ISEEditor-Object.md) objektu.</span><span class="sxs-lookup"><span data-stu-id="f2711-134">The read-only property that gets the Console pane [editor](../ise/The-ISEEditor-Object.md) object.</span></span>

```powershell
# Gets the Console Pane editor.
$psISE.CurrentPowerShellTab.ConsolePane
```

### <a name="displayname"></a><span data-ttu-id="f2711-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="f2711-135">DisplayName</span></span>

<span data-ttu-id="f2711-136">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="f2711-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="f2711-137">Vlastnost pro čtení a zápis, který získá nebo nastaví text, který se zobrazí na kartě prostředí PowerShell. Ve výchozím nastavení, jsou karty s názvem "PowerShell #", kde znak # představuje číslo.</span><span class="sxs-lookup"><span data-stu-id="f2711-137">The read-write property that gets or sets the text that is displayed on the PowerShell tab. By default, tabs are named "PowerShell #", where the # represents a number.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="expandedscript"></a><span data-ttu-id="f2711-138">ExpandedScript</span><span class="sxs-lookup"><span data-stu-id="f2711-138">ExpandedScript</span></span>

<span data-ttu-id="f2711-139">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="f2711-139">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="f2711-140">Pro čtení a zápis vlastnost typu Boolean, která určuje, zda je v podokně skriptu rozšířit nebo skrytý.</span><span class="sxs-lookup"><span data-stu-id="f2711-140">The read-write Boolean property that determines whether the Script pane is expanded or hidden.</span></span>

```powershell
# Toggle the expanded script property to see its effect.
$psISE.CurrentPowerShellTab.ExpandedScript = !$psISE.CurrentPowerShellTab.ExpandedScript
```

### <a name="files"></a><span data-ttu-id="f2711-141">Soubory</span><span class="sxs-lookup"><span data-stu-id="f2711-141">Files</span></span>

<span data-ttu-id="f2711-142">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="f2711-142">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="f2711-143">Vlastnost jen pro čtení, který získá [kolekce souborů skriptů](../ise/The-ISEFileCollection-Object.md) , jsou otevřeny v kartě prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2711-143">The read-only property that gets the [collection of script files](../ise/The-ISEFileCollection-Object.md) that are open in the PowerShell tab.</span></span>

```powershell
$newFile = $psISE.CurrentPowerShellTab.Files.Add()
$newFile.Editor.Text = "a`r`nb"
# Gets the line count
$newFile.Editor.LineCount
```

### <a name="output"></a><span data-ttu-id="f2711-144">Výstup</span><span class="sxs-lookup"><span data-stu-id="f2711-144">Output</span></span>

<span data-ttu-id="f2711-145">Tato funkce je k dispozici v prostředí Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.</span><span class="sxs-lookup"><span data-stu-id="f2711-145">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="f2711-146">V novějších verzích systému Windows PowerShell ISE, můžete použít **ConsolePane** objekt pro stejné účely.</span><span class="sxs-lookup"><span data-stu-id="f2711-146">In later versions of Windows PowerShell ISE, you can use the **ConsolePane** object for the same purposes.</span></span>

<span data-ttu-id="f2711-147">Vlastnost jen pro čtení, který získá podokno výstup aktuálního [editor](../ise/The-ISEEditor-Object.md).</span><span class="sxs-lookup"><span data-stu-id="f2711-147">The read-only property that gets the Output pane of the current [editor](../ise/The-ISEEditor-Object.md).</span></span>

```powershell
# Clears the text in the Output pane.
$psISE.CurrentPowerShellTab.output.clear()
```

### <a name="prompt"></a><span data-ttu-id="f2711-148">řádku</span><span class="sxs-lookup"><span data-stu-id="f2711-148">Prompt</span></span>

<span data-ttu-id="f2711-149">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="f2711-149">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="f2711-150">Vlastnost jen pro čtení, získá aktuální text výzvy.</span><span class="sxs-lookup"><span data-stu-id="f2711-150">The read-only property that gets the current prompt text.</span></span> <span data-ttu-id="f2711-151">Poznámka: **výzva** funkce mohou být přepsány uživatele '™ s profil.</span><span class="sxs-lookup"><span data-stu-id="f2711-151">Note: the **Prompt** function can be overridden by the user'™s profile.</span></span> <span data-ttu-id="f2711-152">Pokud je výsledek než jednoduchý řetězec, pak tato vlastnost vrátí nic.</span><span class="sxs-lookup"><span data-stu-id="f2711-152">If the result is other than a simple string, then this property returns nothing.</span></span>

```powershell
# Gets the current prompt text.
$psISE.CurrentPowerShellTab.Prompt
```

### <a name="showcommands"></a><span data-ttu-id="f2711-153">ShowCommands</span><span class="sxs-lookup"><span data-stu-id="f2711-153">ShowCommands</span></span>

<span data-ttu-id="f2711-154">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="f2711-154">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="f2711-155">Vlastnost pro čtení a zápis, která označuje, pokud je aktuálně zobrazený na panelu příkazů.</span><span class="sxs-lookup"><span data-stu-id="f2711-155">The read-write property that indicates if the Commands pane is currently displayed.</span></span>

```powershell
# Gets the current status of the Commands pane and stores it in the $a variable
$a = $psISE.CurrentPowerShellTab.ShowCommands
# if $a is $false, then turn the Commands pane on by changing the value to $true
if (!$a) {$psISE.CurrentPowerShellTab.ShowCommands = $true}
```

### <a name="statustext"></a><span data-ttu-id="f2711-156">StatusText</span><span class="sxs-lookup"><span data-stu-id="f2711-156">StatusText</span></span>

<span data-ttu-id="f2711-157">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="f2711-157">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="f2711-158">Vlastnost jen pro čtení, který získá **PowerShellTab** stav text.</span><span class="sxs-lookup"><span data-stu-id="f2711-158">The read-only property that gets the **PowerShellTab** status text.</span></span>

```powershell
# Gets the current status text,
$psISE.CurrentPowerShellTab.StatusText
```

### <a name="horizontaladdontoolspaneopened"></a><span data-ttu-id="f2711-159">HorizontalAddOnToolsPaneOpened</span><span class="sxs-lookup"><span data-stu-id="f2711-159">HorizontalAddOnToolsPaneOpened</span></span>

<span data-ttu-id="f2711-160">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="f2711-160">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="f2711-161">Vlastnost jen pro čtení, která určuje, zda je aktuálně otevřených podokna nástrojů horizontální rozšíření.</span><span class="sxs-lookup"><span data-stu-id="f2711-161">The read-only property that indicates whether the horizontal Add-Ons tool pane is currently open.</span></span>

```powershell
# Gets the current state of the horizontal Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

### <a name="verticaladdontoolspaneopened"></a><span data-ttu-id="f2711-162">VerticalAddOnToolsPaneOpened</span><span class="sxs-lookup"><span data-stu-id="f2711-162">VerticalAddOnToolsPaneOpened</span></span>

<span data-ttu-id="f2711-163">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="f2711-163">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="f2711-164">Vlastnost jen pro čtení, která určuje, zda je aktuálně otevřených podokna nástrojů svislé rozšíření.</span><span class="sxs-lookup"><span data-stu-id="f2711-164">The read-only property that indicates whether the vertical Add-Ons tool pane is currently open.</span></span>

```powershell
# Turns on the Commands pane
$psISE.CurrentPowerShellTab.ShowCommands = $true
# Gets the current state of the vertical Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

## <a name="see-also"></a><span data-ttu-id="f2711-165">Viz také</span><span class="sxs-lookup"><span data-stu-id="f2711-165">See Also</span></span>

- [<span data-ttu-id="f2711-166">Objekt PowerShellTabCollection</span><span class="sxs-lookup"><span data-stu-id="f2711-166">The PowerShellTabCollection Object</span></span>](The-PowerShellTabCollection-Object.md)
- [<span data-ttu-id="f2711-167">Účelem ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="f2711-167">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="f2711-168">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="f2711-168">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)