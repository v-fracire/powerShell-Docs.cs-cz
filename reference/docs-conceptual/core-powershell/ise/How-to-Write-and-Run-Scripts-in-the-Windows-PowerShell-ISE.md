---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Psání a spouštění skriptů v prostředí Windows PowerShell ISE
ms.assetid: 62f916d9-b3a1-484a-bdfb-41f57112c22b
ms.openlocfilehash: 4d7c5352ef1dac6f63a50433676068f83a920db5
ms.sourcegitcommit: 735ccab3fb3834ccd8559fab6700b798e8e5ffbf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/25/2018
---
# <a name="how-to-write-and-run-scripts-in-the-windows-powershell-ise"></a><span data-ttu-id="6025e-103">Psání a spouštění skriptů v prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="6025e-103">How to Write and Run Scripts in the Windows PowerShell ISE</span></span>

<span data-ttu-id="6025e-104">Toto téma popisuje, jak vytvořit, upravit, spuštění a uložit skripty v podokně skriptu.</span><span class="sxs-lookup"><span data-stu-id="6025e-104">This topic describes how to create, edit, run, and save scripts in the Script Pane.</span></span>

## <a name="how-to-create-and-run-scripts"></a><span data-ttu-id="6025e-105">Postup vytvoření a spouštět skripty.</span><span class="sxs-lookup"><span data-stu-id="6025e-105">How to create and run scripts</span></span>

<span data-ttu-id="6025e-106">Můžete otevírat a upravovat soubory prostředí Windows PowerShell v podokně skriptu.</span><span class="sxs-lookup"><span data-stu-id="6025e-106">You can open and edit Windows PowerShell files in the Script Pane.</span></span> <span data-ttu-id="6025e-107">Určité typy souborů zájmu v prostředí Windows PowerShell jsou soubory skriptu (.ps1), skript datových souborů (.psd1) a soubory modulu skriptu (.psm1).</span><span class="sxs-lookup"><span data-stu-id="6025e-107">Specific file types of interest in Windows PowerShell are script files (.ps1), script data files (.psd1), and script module files (.psm1).</span></span> <span data-ttu-id="6025e-108">Tyto typy souborů jsou syntaxe barevné v editoru panelu Skript.</span><span class="sxs-lookup"><span data-stu-id="6025e-108">These file types are syntax colored in the Script Pane editor.</span></span> <span data-ttu-id="6025e-109">Další běžné typy souborů, které může zobrazit v podokně skriptu jsou konfigurační soubory (.ps1xml), soubory XML a textové soubory.</span><span class="sxs-lookup"><span data-stu-id="6025e-109">Other common file types you may open in the Script Pane are configuration files (.ps1xml), XML files, and text files.</span></span>

> [!NOTE]
> <span data-ttu-id="6025e-110">Zásady spouštění prostředí Windows PowerShell Určuje, zda můžete spouštět skripty a zatížení profily prostředí Windows PowerShell a konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="6025e-110">The Windows PowerShell execution policy determines whether you can run scripts and load Windows PowerShell profiles and configuration files.</span></span> <span data-ttu-id="6025e-111">Výchozí zásady spouštění, brání spuštění všech skriptů s omezeným přístupem a zabrání načítání profily.</span><span class="sxs-lookup"><span data-stu-id="6025e-111">The default execution policy, Restricted, prevents all scripts from running, and prevents loading profiles.</span></span> <span data-ttu-id="6025e-112">Chcete-li změnit zásady spouštění umožňující profily se načíst a použít, najdete v části [Set-ExecutionPolicy [PSITPro5_Security]](https://technet.microsoft.com/library/5690a0e1-495b-4e63-8280-65ead7bf01ab) a [about_Signing [v4]](https://technet.microsoft.com/library/fcbdd3b9-0b9f-4734-b5c7-e0dcc304fa1d).</span><span class="sxs-lookup"><span data-stu-id="6025e-112">To change the execution policy to allow profiles to load and be used, see [Set-ExecutionPolicy[PSITPro5_Security]](https://technet.microsoft.com/library/5690a0e1-495b-4e63-8280-65ead7bf01ab) and [about_Signing [v4]](https://technet.microsoft.com/library/fcbdd3b9-0b9f-4734-b5c7-e0dcc304fa1d).</span></span>

### <a name="to-create-a-new-script-file"></a><span data-ttu-id="6025e-113">Chcete-li vytvořit nový soubor skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-113">To create a new script file</span></span>

<span data-ttu-id="6025e-114">Na panelu nástrojů klikněte na tlačítko **nový** , nebo na **soubor** nabídky, klikněte na tlačítko **nový**.</span><span class="sxs-lookup"><span data-stu-id="6025e-114">On the toolbar, click **New** , or on the **File** menu, click **New**.</span></span> <span data-ttu-id="6025e-115">Vytvořený soubor se zobrazí na nové záložce souboru na kartě aktuální prostředí PowerShell. Mějte na paměti, že prostředí PowerShell karty jsou viditelné pouze když je více než jeden.</span><span class="sxs-lookup"><span data-stu-id="6025e-115">The created file appears in a new file tab under the current PowerShell tab. Remember that the PowerShell tabs are only visible when there are more than one.</span></span> <span data-ttu-id="6025e-116">Ve výchozím nastavení se vytvoří soubor skriptu typ (.ps1), ale nelze uložit s novým názvem a rozšíření.</span><span class="sxs-lookup"><span data-stu-id="6025e-116">By default a file of type script (.ps1) is created, but it can be saved with a new name and extension.</span></span> <span data-ttu-id="6025e-117">Více souborů skriptu lze vytvořit na stejné kartě prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6025e-117">Multiple script files can be created in the same PowerShell tab.</span></span>

### <a name="to-open-an-existing-script"></a><span data-ttu-id="6025e-118">Chcete-li otevřít existující skript</span><span class="sxs-lookup"><span data-stu-id="6025e-118">To open an existing script</span></span>

<span data-ttu-id="6025e-119">Na panelu nástrojů klikněte na tlačítko **otevřete**, nebo na **soubor** nabídky, klikněte na tlačítko **otevřete**.</span><span class="sxs-lookup"><span data-stu-id="6025e-119">On the toolbar, click **Open**, or on the **File** menu, click **Open**.</span></span> <span data-ttu-id="6025e-120">V **otevřete** dialogové okno, vyberte soubor, který chcete otevřít.</span><span class="sxs-lookup"><span data-stu-id="6025e-120">In the **Open** dialog box, select the file you want to open.</span></span> <span data-ttu-id="6025e-121">Otevřený soubor se zobrazí na nové kartě.</span><span class="sxs-lookup"><span data-stu-id="6025e-121">The opened file appears in a new tab.</span></span>

### <a name="to-close-a-script-tab"></a><span data-ttu-id="6025e-122">Zavřete kartu skript</span><span class="sxs-lookup"><span data-stu-id="6025e-122">To close a script tab</span></span>

<span data-ttu-id="6025e-123">Klikněte na kartu skriptu skriptu, který chcete zavřít, a poté proveďte jednu z následujících akcí:</span><span class="sxs-lookup"><span data-stu-id="6025e-123">Click the script tab of the script you want to close, then do one of the following:</span></span>

1. <span data-ttu-id="6025e-124">Klikněte **Zavřít** ikona (X) na kartě skriptu.</span><span class="sxs-lookup"><span data-stu-id="6025e-124">Click the **Close** icon (X) on the script tab.</span></span>

2. <span data-ttu-id="6025e-125">Na **soubor** nabídky, klikněte na tlačítko **Zavřít**.</span><span class="sxs-lookup"><span data-stu-id="6025e-125">On the **File** menu, click **Close**.</span></span>

<span data-ttu-id="6025e-126">Pokud soubor byla změněna od posledního uložení, zobrazí se výzva k uložte nebo zahoďte ho.</span><span class="sxs-lookup"><span data-stu-id="6025e-126">If the file has been altered since it was last saved, you are prompted to save or discard it.</span></span>

### <a name="to-display-the-file-path"></a><span data-ttu-id="6025e-127">Chcete-li zobrazit cestu k souboru</span><span class="sxs-lookup"><span data-stu-id="6025e-127">To display the file path</span></span>

<span data-ttu-id="6025e-128">Na kartě Soubor přejděte na název souboru.</span><span class="sxs-lookup"><span data-stu-id="6025e-128">On the file tab, point to the file name.</span></span> <span data-ttu-id="6025e-129">Úplná cesta k souboru skriptu se zobrazí ve formě popisu tlačítka.</span><span class="sxs-lookup"><span data-stu-id="6025e-129">The fully qualified path to the script file appears in a tooltip.</span></span>

### <a name="to-run-a-script"></a><span data-ttu-id="6025e-130">Spuštění skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-130">To run a script</span></span>

<span data-ttu-id="6025e-131">Na panelu nástrojů klikněte na tlačítko **spustit skript**, nebo na **soubor** nabídky, klikněte na tlačítko **spustit**.</span><span class="sxs-lookup"><span data-stu-id="6025e-131">On the toolbar, click **Run Script**, or on the **File** menu, click **Run**.</span></span>

### <a name="to-run-a-portion-of-a-script"></a><span data-ttu-id="6025e-132">Ke spuštění část skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-132">To run a portion of a script</span></span>

1. <span data-ttu-id="6025e-133">V podokně skriptu vyberte část skriptu.</span><span class="sxs-lookup"><span data-stu-id="6025e-133">In the Script Pane, select a portion of a script.</span></span>

2. <span data-ttu-id="6025e-134">Na **soubor** nabídky, klikněte na tlačítko **spustit výběr**, nebo na panelu nástrojů klikněte na tlačítko **spustit výběr**.</span><span class="sxs-lookup"><span data-stu-id="6025e-134">On the **File** menu, click **Run Selection**, or on the toolbar, click **Run Selection**.</span></span>

### <a name="to-stop-a-running-script"></a><span data-ttu-id="6025e-135">Zastavit spuštěné skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-135">To stop a running script</span></span>

<span data-ttu-id="6025e-136">Na panelu nástrojů klikněte na tlačítko **zastavit operaci**, stiskněte kombinaci kláves CTRL + BREAK, nebo na **soubor** nabídky, klikněte na tlačítko **zastavit operaci**.</span><span class="sxs-lookup"><span data-stu-id="6025e-136">On the toolbar, click **Stop Operation**, press CTRL+BREAK, or on the **File** menu, click **Stop Operation**.</span></span> <span data-ttu-id="6025e-137">Stisknutím **CTRL + C** funguje taky Pokud některé je aktuálně vybraný text, v takovém případě **CTRL + C** se mapuje na funkci kopírování pro vybraný text.</span><span class="sxs-lookup"><span data-stu-id="6025e-137">Pressing **CTRL+C** also works unless some text is currently selected, in which case **CTRL+C** maps to the copy function for the selected text.</span></span>

## <a name="how-to-write-and-edit-text-in-the-script-pane"></a><span data-ttu-id="6025e-138">Postup zápisu a upravit text v podokně skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-138">How to write and edit text in the Script Pane</span></span>

<span data-ttu-id="6025e-139">Pomocí následujících kroků lze upravit text v podokně skriptu.</span><span class="sxs-lookup"><span data-stu-id="6025e-139">Use the following steps to edit text in the Script Pane.</span></span> <span data-ttu-id="6025e-140">Můžete zkopírovat, Vyjmout, vložte, najít a nahradit text.</span><span class="sxs-lookup"><span data-stu-id="6025e-140">You can copy, cut, paste, find, and replace text.</span></span> <span data-ttu-id="6025e-141">Můžete také vrátit zpět a znovu provést poslední akci, kterou jste právě provedli.</span><span class="sxs-lookup"><span data-stu-id="6025e-141">You can also undo and redo the last action you just performed.</span></span> <span data-ttu-id="6025e-142">Klávesové zkratky pro provádění tyto akce jsou stejné jako pro všechny aplikace systému Windows.</span><span class="sxs-lookup"><span data-stu-id="6025e-142">The keyboard shortcuts for performing these actions are the same as those used for all Windows applications.</span></span>

### <a name="to-enter-text-in-the-script-pane"></a><span data-ttu-id="6025e-143">Zadání textu v podokně skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-143">To enter text in the Script Pane</span></span>

1. <span data-ttu-id="6025e-144">Přesunutí kurzoru do podokna skriptu, klepnutím na libovolné místo v podokně skriptu, nebo klikněte na **přejděte do podokna skriptu** v **zobrazení** nabídky.</span><span class="sxs-lookup"><span data-stu-id="6025e-144">Move the cursor to the Script Pane by clicking anywhere in the Script Pane, or by clicking **Go to Script Pane** in the **View** menu.</span></span>

2. <span data-ttu-id="6025e-145">Vytvořte skript.</span><span class="sxs-lookup"><span data-stu-id="6025e-145">Create a script.</span></span> <span data-ttu-id="6025e-146">Barevné zvýrazňování syntaxe a dokončování pomocí tabulátorů vytvořit bohatší možnosti v systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="6025e-146">Syntax coloring and tab completion make this a richer experience in Windows PowerShell ISE.</span></span>

3. <span data-ttu-id="6025e-147">V tématu [postup dokončování pomocí tabulátorů použijte v skriptu podokně a podokně konzoly](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) podrobnosti o použití funkci doplňování karta při zadání.</span><span class="sxs-lookup"><span data-stu-id="6025e-147">See [How to Use Tab Completion in the Script Pane and Console Pane](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) for details about using the tab completion feature to help in typing.</span></span>

### <a name="to-find-text-in-the-script-pane"></a><span data-ttu-id="6025e-148">Najít text v podokně skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-148">To find text in the Script Pane</span></span>

1. <span data-ttu-id="6025e-149">Chcete-li najít text kdekoli, stiskněte **CTRL + F** nebo na **upravit** nabídky, klikněte na tlačítko **najít ve skriptu**.</span><span class="sxs-lookup"><span data-stu-id="6025e-149">To find text anywhere, press **CTRL+F** or, on the **Edit** menu, click **Find in Script**.</span></span>

2. <span data-ttu-id="6025e-150">Chcete-li najít text po kurzor, stiskněte **F3** nebo na **upravit** nabídky, klikněte na tlačítko **najít další ve skriptu**.</span><span class="sxs-lookup"><span data-stu-id="6025e-150">To find text after the cursor, press **F3** or, on the **Edit** menu, click **Find Next in Script**.</span></span>

3. <span data-ttu-id="6025e-151">Chcete-li najít text před kurzor, stiskněte **SHIFT + F3** nebo na **upravit** nabídky, klikněte na tlačítko **najít předchozí ve skriptu**.</span><span class="sxs-lookup"><span data-stu-id="6025e-151">To find text before the cursor, press **SHIFT+F3** or, on the **Edit** menu, click **Find Previous in Script**.</span></span>

### <a name="to-find-and-replace-text-in-the-script-pane"></a><span data-ttu-id="6025e-152">K vyhledání a nahrazení textu v podokně skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-152">To find and replace text in the Script Pane</span></span>

<span data-ttu-id="6025e-153">Stiskněte klávesu **CTRL + H** nebo na **upravit** nabídky, klikněte na tlačítko **nahradit ve skriptu**.</span><span class="sxs-lookup"><span data-stu-id="6025e-153">Press **CTRL+H** or, on the **Edit** menu, click **Replace in Script**.</span></span> <span data-ttu-id="6025e-154">Zadejte text, který chcete najít a text, pro který chcete nahradit, a potom stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="6025e-154">Enter both the text you want to find and the text with which you want to replace it, and then press **ENTER**.</span></span>

### <a name="to-go-to-a-particular-line-of-text-in-the-script-pane"></a><span data-ttu-id="6025e-155">Přejít na konkrétní řádku textu v podokně skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-155">To go to a particular line of text in the Script Pane</span></span>

1. <span data-ttu-id="6025e-156">V podokně skriptu stiskněte **kombinaci kláves CTRL + G** nebo na **upravit** nabídky, klikněte na tlačítko **přechod na řádek**.</span><span class="sxs-lookup"><span data-stu-id="6025e-156">In the Script Pane, press **CTRL+G** or, on the **Edit** menu, click **Go to Line**.</span></span>

2. <span data-ttu-id="6025e-157">Zadejte číslo řádku.</span><span class="sxs-lookup"><span data-stu-id="6025e-157">Enter a line number.</span></span>

### <a name="to-copy-text-in-the-script-pane"></a><span data-ttu-id="6025e-158">Zkopírujte text v podokně skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-158">To copy text in the Script Pane</span></span>

1. <span data-ttu-id="6025e-159">V podokně skriptu vyberte text, který chcete zkopírovat.</span><span class="sxs-lookup"><span data-stu-id="6025e-159">In the Script Pane, select the text that you want to copy.</span></span>

2. <span data-ttu-id="6025e-160">Stiskněte klávesu **CTRL + C** nebo na panelu nástrojů klikněte na tlačítko **kopie** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **kopie**.</span><span class="sxs-lookup"><span data-stu-id="6025e-160">Press **CTRL+C** or, on the toolbar, click the **Copy** icon, or on the **Edit** menu, click **Copy**.</span></span>

### <a name="to-cut-text-in-the-script-pane"></a><span data-ttu-id="6025e-161">Vyjímání text v podokně skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-161">To cut text in the Script Pane</span></span>

1. <span data-ttu-id="6025e-162">V podokně skriptu vyberte text, který chcete vyjmout.</span><span class="sxs-lookup"><span data-stu-id="6025e-162">In the Script Pane, select the text that you want to cut.</span></span>

2. <span data-ttu-id="6025e-163">Stiskněte klávesu **CTRL + X** nebo na panelu nástrojů klikněte na tlačítko **Vyjmout** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **Vyjmout**.</span><span class="sxs-lookup"><span data-stu-id="6025e-163">Press **CTRL+X** or, on the toolbar, click the **Cut** icon, or on the **Edit** menu, click **Cut**.</span></span>

### <a name="to-paste-text-into-the-script-pane"></a><span data-ttu-id="6025e-164">Chcete vložit text do podokna skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-164">To paste text into the Script Pane</span></span>

<span data-ttu-id="6025e-165">Stiskněte klávesu **CTRL + V** nebo na panelu nástrojů klikněte na tlačítko **vložení** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **vložení**.</span><span class="sxs-lookup"><span data-stu-id="6025e-165">Press **CTRL+V** or, on the toolbar, click the **Paste** icon, or on the **Edit** menu, click **Paste**.</span></span>

### <a name="to-undo-an-action-in-the-script-pane"></a><span data-ttu-id="6025e-166">Postup vrácení akce v podokně skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-166">To undo an action in the Script Pane</span></span>

<span data-ttu-id="6025e-167">Stiskněte klávesu **CTRL + Z** nebo na panelu nástrojů klikněte na tlačítko **vrátit zpět** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **vrátit zpět**.</span><span class="sxs-lookup"><span data-stu-id="6025e-167">Press **CTRL+Z** or, on the toolbar, click the **Undo** icon, or on the **Edit** menu, click **Undo**.</span></span>

### <a name="to-redo-an-action-in-the-script-pane"></a><span data-ttu-id="6025e-168">Opakování akce v podokně skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-168">To redo an action in the Script Pane</span></span>

<span data-ttu-id="6025e-169">Stiskněte klávesu **CTRL + Y** nebo na panelu nástrojů klikněte na tlačítko **vrátit** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **vrátit**.</span><span class="sxs-lookup"><span data-stu-id="6025e-169">Press **CTRL+Y** or, on the toolbar, click the **Redo** icon, or on the **Edit** menu, click **Redo**.</span></span>

## <a name="how-to-save-a-script"></a><span data-ttu-id="6025e-170">Jak uložit skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-170">How to save a script</span></span>

<span data-ttu-id="6025e-171">Pomocí následujících kroků pro uložení a název skriptu.</span><span class="sxs-lookup"><span data-stu-id="6025e-171">Use the following steps to save and name a script.</span></span> <span data-ttu-id="6025e-172">Vedle názvu skriptu k označení soubor, který ještě nebyl uložen, protože byla změněna se zobrazuje hvězdička.</span><span class="sxs-lookup"><span data-stu-id="6025e-172">An asterisk appears next to the script name to mark a file that has not been saved since it was altered.</span></span> <span data-ttu-id="6025e-173">Hvězdička zmizí při uložení souboru.</span><span class="sxs-lookup"><span data-stu-id="6025e-173">The asterisk disappears when the file is saved.</span></span>

### <a name="to-save-a-script"></a><span data-ttu-id="6025e-174">Uložte skript</span><span class="sxs-lookup"><span data-stu-id="6025e-174">To save a script</span></span>

<span data-ttu-id="6025e-175">Stiskněte klávesu **CTRL + S** nebo na panelu nástrojů klikněte na tlačítko **Uložit** ikonu, nebo na **soubor** nabídky, klikněte na tlačítko **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="6025e-175">Press **CTRL+S** or, on the toolbar, click the **Save** icon, or on the **File** menu, click **Save**.</span></span>

### <a name="to-save-and-name-a-script"></a><span data-ttu-id="6025e-176">Uložte a název skriptu</span><span class="sxs-lookup"><span data-stu-id="6025e-176">To save and name a script</span></span>

1. <span data-ttu-id="6025e-177">Na **soubor** nabídky, klikněte na tlačítko **uložit jako**.</span><span class="sxs-lookup"><span data-stu-id="6025e-177">On the **File** menu, click **Save As**.</span></span> <span data-ttu-id="6025e-178">**Uložit jako** se zobrazí dialogové okno.</span><span class="sxs-lookup"><span data-stu-id="6025e-178">The **Save As** dialog box will appear.</span></span>

2. <span data-ttu-id="6025e-179">V **název souboru** pole, zadejte název souboru.</span><span class="sxs-lookup"><span data-stu-id="6025e-179">In the **File name** box, enter a name for the file.</span></span>

3. <span data-ttu-id="6025e-180">V **uložit jako typ** , vyberte typ souboru.</span><span class="sxs-lookup"><span data-stu-id="6025e-180">In the **Save as type** box, select a file type.</span></span> <span data-ttu-id="6025e-181">Například v **uložit jako typ** vyberte ' œPowerShell skripty (\* .ps1)'.</span><span class="sxs-lookup"><span data-stu-id="6025e-181">For example, in the **Save as type** box, select 'œPowerShell Scripts (\* .ps1)'.</span></span>

4. <span data-ttu-id="6025e-182">Klikněte na **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="6025e-182">Click **Save**.</span></span>

### <a name="to-save-a-script-in-ascii-encoding"></a><span data-ttu-id="6025e-183">Uložte skript v kódování ASCII</span><span class="sxs-lookup"><span data-stu-id="6025e-183">To save a script in ASCII encoding</span></span>

<span data-ttu-id="6025e-184">Ve výchozím nastavení Windows PowerShell ISE uloží nové soubory skriptu (.ps1), skript datových souborů (.psd1) a soubory modulu skriptu (.psm1) jako Unicode (BigEndianUnicode) ve výchozím nastavení. Některá k uložení skript v jiné kódování, jako je například ASCII (ANSI), použijte **Uložit** nebo **uložit jako** metody [$psISE.CurrentFile](https://technet.microsoft.com/library/bc3300e4-9c17-4f00-a621-c8867126e3b3#CurrentFile) objektu.</span><span class="sxs-lookup"><span data-stu-id="6025e-184">By default, Windows PowerShell ISE saves new script files (.ps1), script data files (.psd1), and script module files (.psm1) as Unicode (BigEndianUnicode) by default.Â To save a script in another encoding, such as ASCII (ANSI), use the **Save** or **SaveAs** methods on the [$psISE.CurrentFile](https://technet.microsoft.com/library/bc3300e4-9c17-4f00-a621-c8867126e3b3#CurrentFile) object.</span></span>

<span data-ttu-id="6025e-185">Následující příkaz uloží nový skript jako MyScript.ps1 s kódováním ASCII.</span><span class="sxs-lookup"><span data-stu-id="6025e-185">The following command saves a new script as MyScript.ps1 with ASCII encoding.</span></span>

```powershell
$psISE.CurrentFile.SaveAs("MyScript.ps1", [System.Text.Encoding]::ASCII)
```

<span data-ttu-id="6025e-186">Následující příkaz nahradí aktuální soubor skriptu soubor se stejným názvem, ale s kódováním ASCII.</span><span class="sxs-lookup"><span data-stu-id="6025e-186">The following command replaces the current script file with a file with the same name, but with ASCII encoding.</span></span>

```powershell
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)
```

<span data-ttu-id="6025e-187">Následující příkaz získá kódování aktuálního souboru.</span><span class="sxs-lookup"><span data-stu-id="6025e-187">The following command gets the encoding of the current file.</span></span>

```powershell
$psISE.CurrentFile.encoding
```

<span data-ttu-id="6025e-188">Windows PowerShell ISE podporuje následující možnosti kódování: ASCII, BigEndianUnicode, kódování Unicode, UTF32, UTF7, UTF8 a výchozí.</span><span class="sxs-lookup"><span data-stu-id="6025e-188">Windows PowerShell ISE supports the following encoding options: ASCII, BigEndianUnicode, Unicode, UTF32, UTF7, UTF8 and Default.</span></span> <span data-ttu-id="6025e-189">Hodnota výchozí možnost se liší podle systému.</span><span class="sxs-lookup"><span data-stu-id="6025e-189">The value of the Default option varies with the system.</span></span>

<span data-ttu-id="6025e-190">Windows PowerShell ISE nezmění kódování skripty, které byly vytvořené v jiných editory, i když použijete uložit nebo uložit jako příkazů v systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="6025e-190">Windows PowerShell ISE does not change the encoding of scripts that were created by in other editors, even when you use the Save or Save As commands in Windows PowerShell ISE.</span></span>

## <a name="see-also"></a><span data-ttu-id="6025e-191">Viz také</span><span class="sxs-lookup"><span data-stu-id="6025e-191">See Also</span></span>

- [<span data-ttu-id="6025e-192">Seznámení s prostředím Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="6025e-192">Exploring the Windows PowerShell ISE</span></span>](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)