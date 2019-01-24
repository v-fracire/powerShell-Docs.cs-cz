---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Seznámení s prostředím Windows PowerShell ISE
ms.assetid: e0d2c6e8-5126-40e7-a1e1-d1cff29fe94a
ms.openlocfilehash: 059651f159fb2636a93167709134788e90d062b8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403865"
---
# <a name="exploring-the-windows-powershell-ise"></a><span data-ttu-id="6fe0f-103">Seznámení s prostředím Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="6fe0f-103">Exploring the Windows PowerShell ISE</span></span>

<span data-ttu-id="6fe0f-104">Windows PowerShell® integrovaném skriptovacím prostředí (ISE) můžete použít k vytvoření, spuštění a ladění příkazy a skripty.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-104">You can use the Windows PowerShell® Integrated Scripting Environment (ISE) to create, run, and debug commands and scripts.</span></span> <span data-ttu-id="6fe0f-105">Windows PowerShell ISE se skládá z řádku nabídek, karty prostředí Windows PowerShell, panelu nástrojů, skript karty, podokno skriptu, podokně konzoly, stavového řádku, posuvník velikost textu a kontextové nápovědy.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-105">The Windows PowerShell ISE consists of the menu bar, Windows PowerShell tabs, the toolbar, script tabs, a Script Pane, a Console Pane, a status bar, a text-size slider and context-sensitive Help.</span></span>

> [!NOTE]
> <span data-ttu-id="6fe0f-106">Od verze 3.0 ISE Windows Powershellu příkaz a výstupní podokna byly sloučeny do jediného konzoly.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-106">Beginning with Windows PowerShell ISE 3.0 the Command and Output Panes were combined into a single Console Pane.</span></span>

## <a name="menu-bar"></a><span data-ttu-id="6fe0f-107">Panel nabídek</span><span class="sxs-lookup"><span data-stu-id="6fe0f-107">Menu Bar</span></span>

<span data-ttu-id="6fe0f-108">Panel nabídek obsahuje **souboru**, **upravit**, **zobrazení**, **nástroje**, **ladění**,  **Doplňky**, a **pomáhají** nabídky.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-108">The menu bar contains the **File**, **Edit**, **View**, **Tools**, **Debug**, **Add-ons**, and **Help** menus.</span></span> <span data-ttu-id="6fe0f-109">Tlačítka v nabídkách umožňují provádět úlohy související s psaní a spuštěných skriptů a spouštění příkazů v prostředí Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-109">The buttons on the menus allow you to perform tasks related to writing and running scripts and running commands in the Windows PowerShell ISE.</span></span> <span data-ttu-id="6fe0f-110">Kromě toho [doplněk Nástroje](../../core-powershell/ise/The-ISEAddOnTool-Object.md) můžete umístit na řádku nabídek díky spouštění skriptů, které používají [The hierarchie objektového modelu prostředí ISE](../../core-powershell/ise/The-ISE-Object-Model-Hierarchy.md).</span><span class="sxs-lookup"><span data-stu-id="6fe0f-110">Additionally, an [add-on tool](../../core-powershell/ise/The-ISEAddOnTool-Object.md) may be placed on the menu bar by running scripts that use the [The ISE Object Model Hierarchy](../../core-powershell/ise/The-ISE-Object-Model-Hierarchy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6fe0f-111">Ve Windows PowerShell ISE 2.0 **nástroje** a **doplňky** nabídky nebyly k dispozici.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-111">In Windows PowerShell ISE 2.0, The **Tools** and **Add-ons** menus were not present.</span></span>

## <a name="windows-powershell-tabs"></a><span data-ttu-id="6fe0f-112">Karty Windows Powershellu</span><span class="sxs-lookup"><span data-stu-id="6fe0f-112">Windows PowerShell Tabs</span></span>

<span data-ttu-id="6fe0f-113">Karta prostředí Windows PowerShell je prostředí, ve kterém se spustí skript Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-113">A Windows PowerShell tab is the environment in which a Windows PowerShell script runs.</span></span> <span data-ttu-id="6fe0f-114">Nové karty v prostředí Windows PowerShell můžete otevřít v prostředí Windows PowerShell ISE vytvořit samostatná prostředí v místním počítači nebo na vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-114">You can open new Windows PowerShell tabs in the Windows PowerShell ISE to create separate environments on your local computer or on remote computers.</span></span> <span data-ttu-id="6fe0f-115">Může mít maximálně osm Powershellu karty najednou otevřít.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-115">You may have a maximum of eight PowerShell tabs simultaneously open.</span></span>

## <a name="toolbar"></a><span data-ttu-id="6fe0f-116">Panel nástrojů</span><span class="sxs-lookup"><span data-stu-id="6fe0f-116">Toolbar</span></span>

<span data-ttu-id="6fe0f-117">Následující tlačítka jsou umístěny na panelu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-117">The following buttons are located on the toolbar.</span></span>

|<span data-ttu-id="6fe0f-118">Tlačítko</span><span class="sxs-lookup"><span data-stu-id="6fe0f-118">Button</span></span>|<span data-ttu-id="6fe0f-119">Funkce</span><span class="sxs-lookup"><span data-stu-id="6fe0f-119">Function</span></span>|
|----------|------------|
|<span data-ttu-id="6fe0f-120">**Nový**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-120">**New**</span></span>|<span data-ttu-id="6fe0f-121">Otevře se nový skript.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-121">Opens a new script.</span></span>|
|<span data-ttu-id="6fe0f-122">**Otevřít**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-122">**Open**</span></span>|<span data-ttu-id="6fe0f-123">Otevře existující skriptu nebo soubor.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-123">Opens an existing script or file.</span></span>|
|<span data-ttu-id="6fe0f-124">**Uložení**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-124">**Save**</span></span>|<span data-ttu-id="6fe0f-125">Uloží skriptu nebo soubor.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-125">Saves a script or file.</span></span>|
|<span data-ttu-id="6fe0f-126">**Vyjmout**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-126">**Cut**</span></span>|<span data-ttu-id="6fe0f-127">Vyjme vybraný text a zkopíruje do schránky.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-127">Cuts the selected text and copies it to the clipboard.</span></span>|
|<span data-ttu-id="6fe0f-128">**Kopírování**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-128">**Copy**</span></span>|<span data-ttu-id="6fe0f-129">Zkopíruje vybraný text do schránky.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-129">Copies the selected text to the clipboard.</span></span>|
|<span data-ttu-id="6fe0f-130">**Vložit**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-130">**Paste**</span></span>|<span data-ttu-id="6fe0f-131">Vloží obsah schránky do umístění kurzoru.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-131">Pastes the contents of the clipboard at the cursor location.</span></span>|
|<span data-ttu-id="6fe0f-132">**Vymazat podokno výstup**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-132">**Clear Output Pane**</span></span>|<span data-ttu-id="6fe0f-133">Vymaže veškerý obsah v podokně výstup.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-133">Clears all content in the Output Pane.</span></span>|
|<span data-ttu-id="6fe0f-134">**Vrácení zpět**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-134">**Undo**</span></span>|<span data-ttu-id="6fe0f-135">Obrátí akci, která se právě provedla.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-135">Reverses the action that was just performed.</span></span>|
|<span data-ttu-id="6fe0f-136">**Znovu:**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-136">**Redo**</span></span>|<span data-ttu-id="6fe0f-137">Provede akci, která byla právě vrátit zpět.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-137">Performs the action that was just undone.</span></span>|
|<span data-ttu-id="6fe0f-138">**Spuštění skriptu**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-138">**Run Script**</span></span>|<span data-ttu-id="6fe0f-139">Spustí skript.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-139">Runs a script.</span></span>|
|<span data-ttu-id="6fe0f-140">**Spustit výběr**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-140">**Run Selection**</span></span>|<span data-ttu-id="6fe0f-141">Spustí vybranou část skriptu.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-141">Runs a selected portion of a script.</span></span>|
|<span data-ttu-id="6fe0f-142">**Zastavit provádění**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-142">**Stop Execution**</span></span>|<span data-ttu-id="6fe0f-143">Zastaví skript, který je spuštěn.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-143">Stops a script that is running.</span></span>|
|<span data-ttu-id="6fe0f-144">**Nová karta vzdáleného prostředí PowerShell**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-144">**New Remote PowerShell Tab**</span></span>|<span data-ttu-id="6fe0f-145">Vytvoří nová karta prostředí PowerShell, který vytvoří relaci ve vzdáleném počítači.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-145">Creates a new PowerShell Tab that establishes a session on a remote computer.</span></span> <span data-ttu-id="6fe0f-146">Dialogové okno se zobrazí a zobrazí výzvu k zadání podrobností, které jsou potřebné k navázání vzdáleného připojení.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-146">A dialog box appears and prompts you to enter details required to establish the remote connection.</span></span>|
|<span data-ttu-id="6fe0f-147">**Spustit PowerShell.exe**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-147">**Start PowerShell.exe**</span></span>|<span data-ttu-id="6fe0f-148">Otevře se konzola Powershellu.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-148">Opens a PowerShell Console.</span></span>|
|<span data-ttu-id="6fe0f-149">**Zobrazit horní podokno skriptu**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-149">**Show Script Pane Top**</span></span>|<span data-ttu-id="6fe0f-150">V podokně skriptu přesune do horní části v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-150">Moves the Script Pane to the top in the display.</span></span>|
|<span data-ttu-id="6fe0f-151">**Zobrazit podokno skriptu vpravo**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-151">**Show Script Pane Right**</span></span>|<span data-ttu-id="6fe0f-152">Posune podokno skriptu vpravo v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-152">Moves the Script Pane to the right in the display.</span></span>|
|<span data-ttu-id="6fe0f-153">**Zobrazit podokno skriptu maximalizované**</span><span class="sxs-lookup"><span data-stu-id="6fe0f-153">**Show Script Pane Maximized**</span></span>|<span data-ttu-id="6fe0f-154">Maximalizuje v podokně skriptu.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-154">Maximizes the Script Pane.</span></span>|

## <a name="script-tab"></a><span data-ttu-id="6fe0f-155">Karta skriptu</span><span class="sxs-lookup"><span data-stu-id="6fe0f-155">Script Tab</span></span>

<span data-ttu-id="6fe0f-156">Název skriptu, který upravujete.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-156">Displays the name of the script you are editing.</span></span> <span data-ttu-id="6fe0f-157">Můžete kliknout na kartu skript vyberte skript, který chcete upravit.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-157">You can click a script tab to select the script you want to edit.</span></span>

<span data-ttu-id="6fe0f-158">Když přejdete na kartu skript, plně kvalifikovanou cestu k souboru skriptu se zobrazí v popisku.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-158">When you point to the script tab, the fully qualified path to the script file appears in a tooltip.</span></span>

## <a name="script-pane"></a><span data-ttu-id="6fe0f-159">Podokno skriptu</span><span class="sxs-lookup"><span data-stu-id="6fe0f-159">Script Pane</span></span>

<span data-ttu-id="6fe0f-160">Umožňuje vytvářet a spouštět skripty.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-160">Allows you to create and run scripts.</span></span> <span data-ttu-id="6fe0f-161">Můžete otevřít, upravit a spustit stávající skripty v podokně skriptu.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-161">You can open, edit and run existing scripts in the Script Pane.</span></span>

## <a name="output-pane"></a><span data-ttu-id="6fe0f-162">Podokno výstup</span><span class="sxs-lookup"><span data-stu-id="6fe0f-162">Output Pane</span></span>

<span data-ttu-id="6fe0f-163">Zobrazí výsledky příkazy a skripty, které jste spustili.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-163">Displays the results of the commands and scripts you have run.</span></span> <span data-ttu-id="6fe0f-164">Můžete také zkopírovat a vymazat obsah v podokně výstup.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-164">You can also copy and clear the contents in the Output Pane.</span></span>

## <a name="command-pane"></a><span data-ttu-id="6fe0f-165">Příkazového podokna</span><span class="sxs-lookup"><span data-stu-id="6fe0f-165">Command Pane</span></span>

<span data-ttu-id="6fe0f-166">Umožňuje psát příkazy.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-166">Allows you to write commands.</span></span> <span data-ttu-id="6fe0f-167">Můžete spustit příkaz jeden řádek nebo víceřádkové příkazu v příkazovém podokně.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-167">You can run a one line command or a multiline command in the Command Pane.</span></span> <span data-ttu-id="6fe0f-168">Stiskněte SHIFT + ENTER každý řádek víceřádkové příkaz a stiskněte klávesu ENTER po poslední řádek ke spuštění příkazu víceřádkový.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-168">Press SHIFT+ENTER to enter each line of a multiline command, and press ENTER after the last line to execute the multiline command.</span></span> <span data-ttu-id="6fe0f-169">Řádku zobrazit nad v příkazovém podokně zobrazuje cestu k aktuálnímu pracovnímu adresáři.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-169">The prompt displayed on top of the Command Pane shows the path to the current working directory.</span></span>

## <a name="status-bar"></a><span data-ttu-id="6fe0f-170">Stavový řádek</span><span class="sxs-lookup"><span data-stu-id="6fe0f-170">Status Bar</span></span>

<span data-ttu-id="6fe0f-171">Umožňuje zobrazit, zda jsou příkazy a skripty, které můžete spouštět kompletní.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-171">Allows you to see whether the commands and scripts that you run are complete.</span></span> <span data-ttu-id="6fe0f-172">Stavový řádek je úplně dole v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-172">The status bar is at the very bottom of the display.</span></span> <span data-ttu-id="6fe0f-173">Vybrané části chybové zprávy se zobrazují na stavovém řádku.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-173">Selected portions of error messages are displayed on the status bar.</span></span>

## <a name="text-size-slider"></a><span data-ttu-id="6fe0f-174">Velikost textu posuvníku</span><span class="sxs-lookup"><span data-stu-id="6fe0f-174">Text-Size Slider</span></span>

<span data-ttu-id="6fe0f-175">Zvětší nebo zmenší velikost textu na obrazovce.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-175">Increases or decreases the size of the text on the screen.</span></span>

## <a name="help"></a><span data-ttu-id="6fe0f-176">Nápověda</span><span class="sxs-lookup"><span data-stu-id="6fe0f-176">Help</span></span>

<span data-ttu-id="6fe0f-177">Nápověda prostředí Windows PowerShell ISE je dostupné na webu v knihovně TechNet.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-177">Help for Windows PowerShell ISE is available on the Web in the TechNet Library.</span></span> <span data-ttu-id="6fe0f-178">Nápovědy můžete otevřít kliknutím **nápovědu k prostředí Windows PowerShell ISE** na **pomáhají** nabídky nebo stisknutím klávesy F1 kdekoli s výjimkou případů, když je kurzor na název rutiny v podokně skriptu nebo konzole.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-178">You can open the Help by clicking **Windows PowerShell ISE Help** on the **Help** menu or by pressing the F1 key anywhere except when the cursor is on a cmdlet name in either the Script Pane or the Console Pane.</span></span> <span data-ttu-id="6fe0f-179">Z **pomáhají** nabídky můžete taky spustit rutinu Update-Help a zobrazit příkazové okno, které vám pomůže při konstrukci příkazy zobrazující všechny parametry rutiny a povolením můžete vyplnit parametry v Formulář snadným ovládáním.</span><span class="sxs-lookup"><span data-stu-id="6fe0f-179">From the **Help** menu you can also run the Update-Help cmdlet, and display the Command Window which assists you in constructing commands by showing you all of the parameters for a cmdlet and enabling you to fill in the parameters in an easy-to-use form.</span></span>

## <a name="see-also"></a><span data-ttu-id="6fe0f-180">Viz také</span><span class="sxs-lookup"><span data-stu-id="6fe0f-180">See Also</span></span>

- [<span data-ttu-id="6fe0f-181">Představení Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="6fe0f-181">Introducing the Windows PowerShell ISE</span></span>](../../core-powershell/ise/Introducing-the-Windows-PowerShell-ISE.md)