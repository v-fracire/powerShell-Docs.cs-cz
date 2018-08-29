---
ms.date: 08/14/2018
keywords: rutiny prostředí PowerShell
title: Psání a spouštění skriptů v prostředí Windows PowerShell ISE
ms.assetid: 62f916d9-b3a1-484a-bdfb-41f57112c22b
ms.openlocfilehash: 943752df2ecd3fce715dda0ca7ade97186620560
ms.sourcegitcommit: 56b9be8503a5a1342c0b85b36f5ba6f57c281b63
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/21/2018
ms.locfileid: "43133821"
---
# <a name="how-to-write-and-run-scripts-in-the-windows-powershell-ise"></a><span data-ttu-id="498df-103">Psání a spouštění skriptů v prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="498df-103">How to Write and Run Scripts in the Windows PowerShell ISE</span></span>

<span data-ttu-id="498df-104">Tento článek popisuje, jak vytvořit, upravit, spustit a uložit skripty v podokně skriptu.</span><span class="sxs-lookup"><span data-stu-id="498df-104">This article describes how to create, edit, run, and save scripts in the Script Pane.</span></span>

## <a name="how-to-create-and-run-scripts"></a><span data-ttu-id="498df-105">Jak vytvořit a spustit skripty</span><span class="sxs-lookup"><span data-stu-id="498df-105">How to create and run scripts</span></span>

<span data-ttu-id="498df-106">Můžete otevřít a upravit soubory prostředí Windows PowerShell v podokně skriptu.</span><span class="sxs-lookup"><span data-stu-id="498df-106">You can open and edit Windows PowerShell files in the Script Pane.</span></span> <span data-ttu-id="498df-107">Určité typy souborů zájmu v prostředí Windows PowerShell jsou soubory skriptů (.ps1), datové soubory skriptu (.psd1) a soubory modulu skriptu (.psm1).</span><span class="sxs-lookup"><span data-stu-id="498df-107">Specific file types of interest in Windows PowerShell are script files (.ps1), script data files (.psd1), and script module files (.psm1).</span></span> <span data-ttu-id="498df-108">Tyto typy souborů se syntaxe zobrazí v podokně se skriptem editoru.</span><span class="sxs-lookup"><span data-stu-id="498df-108">These file types are syntax colored in the Script Pane editor.</span></span> <span data-ttu-id="498df-109">Další běžné typy souborů, které můžete otevřít z podokna skriptu jsou konfigurační soubory (.ps1xml), soubory XML a textové soubory.</span><span class="sxs-lookup"><span data-stu-id="498df-109">Other common file types you may open in the Script Pane are configuration files (.ps1xml), XML files, and text files.</span></span>

> [!NOTE]
> <span data-ttu-id="498df-110">Zásady spouštění prostředí Windows PowerShell Určuje, zda můžete spustit skripty a načíst profily prostředí Windows PowerShell a konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="498df-110">The Windows PowerShell execution policy determines whether you can run scripts and load Windows PowerShell profiles and configuration files.</span></span> <span data-ttu-id="498df-111">Výchozí zásadu spouštění, brání spuštění všech skriptů s omezeným přístupem a brání načítání profilů.</span><span class="sxs-lookup"><span data-stu-id="498df-111">The default execution policy, Restricted, prevents all scripts from running, and prevents loading profiles.</span></span> <span data-ttu-id="498df-112">Chcete-li změnit zásady spouštění povolit profily a načíst a použít, najdete v článku [Set-ExecutionPolicy](/powershell/module/microsoft.powershell.security/set-executionpolicy) a [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing).</span><span class="sxs-lookup"><span data-stu-id="498df-112">To change the execution policy to allow profiles to load and be used, see [Set-ExecutionPolicy](/powershell/module/microsoft.powershell.security/set-executionpolicy) and [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing).</span></span>

### <a name="to-create-a-new-script-file"></a><span data-ttu-id="498df-113">Chcete-li vytvořit nový soubor skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-113">To create a new script file</span></span>

<span data-ttu-id="498df-114">Na panelu nástrojů klikněte na tlačítko **nový**, nebo **souboru** nabídky, klikněte na tlačítko **nový**.</span><span class="sxs-lookup"><span data-stu-id="498df-114">On the toolbar, click **New**, or on the **File** menu, click **New**.</span></span> <span data-ttu-id="498df-115">Vytvořený soubor se zobrazí na nové kartě souboru na aktuální kartě prostředí PowerShell. Mějte na paměti, že karty Powershellu se zobrazují pouze když existuje více než jedna.</span><span class="sxs-lookup"><span data-stu-id="498df-115">The created file appears in a new file tab under the current PowerShell tab. Remember that the PowerShell tabs are only visible when there are more than one.</span></span> <span data-ttu-id="498df-116">Ve výchozím nastavení se vytvoří soubor typ skriptu (.ps1), ale může být uložen s novým názvem a příponou.</span><span class="sxs-lookup"><span data-stu-id="498df-116">By default a file of type script (.ps1) is created, but it can be saved with a new name and extension.</span></span> <span data-ttu-id="498df-117">Na stejné kartě Powershellu lze vytvořit více souborů skriptu.</span><span class="sxs-lookup"><span data-stu-id="498df-117">Multiple script files can be created in the same PowerShell tab.</span></span>

### <a name="to-open-an-existing-script"></a><span data-ttu-id="498df-118">Chcete-li otevřít existující skript</span><span class="sxs-lookup"><span data-stu-id="498df-118">To open an existing script</span></span>

<span data-ttu-id="498df-119">Na panelu nástrojů klikněte na tlačítko **otevřít**, nebo na **souboru** nabídky, klikněte na tlačítko **otevřít**.</span><span class="sxs-lookup"><span data-stu-id="498df-119">On the toolbar, click **Open**, or on the **File** menu, click **Open**.</span></span> <span data-ttu-id="498df-120">V **otevřete** dialogového okna, vyberte soubor, který chcete otevřít.</span><span class="sxs-lookup"><span data-stu-id="498df-120">In the **Open** dialog box, select the file you want to open.</span></span> <span data-ttu-id="498df-121">Otevřený soubor se zobrazí na nové záložce.</span><span class="sxs-lookup"><span data-stu-id="498df-121">The opened file appears in a new tab.</span></span>

### <a name="to-close-a-script-tab"></a><span data-ttu-id="498df-122">Zavřete kartu skript</span><span class="sxs-lookup"><span data-stu-id="498df-122">To close a script tab</span></span>

<span data-ttu-id="498df-123">Klikněte na tlačítko **zavřete** ikonu (X) karty souboru, kterou chcete zavřít nebo vyberte **souboru** nabídky a klikněte na tlačítko **zavřete**.</span><span class="sxs-lookup"><span data-stu-id="498df-123">Click the **Close** icon (X) of the file tab you want to close or select the **File** menu and click **Close**.</span></span>

<span data-ttu-id="498df-124">Pokud soubor byl změněn od posledního uložení, budete vyzváni k ukládání nebo zahazování ho.</span><span class="sxs-lookup"><span data-stu-id="498df-124">If the file has been altered since it was last saved, you're prompted to save or discard it.</span></span>

### <a name="to-display-the-file-path"></a><span data-ttu-id="498df-125">Chcete-li zobrazit cestu k souboru</span><span class="sxs-lookup"><span data-stu-id="498df-125">To display the file path</span></span>

<span data-ttu-id="498df-126">Na kartě souborů odkazovat na název souboru.</span><span class="sxs-lookup"><span data-stu-id="498df-126">On the file tab, point to the file name.</span></span> <span data-ttu-id="498df-127">V popisku se zobrazí plně kvalifikovanou cestu k souboru skriptu.</span><span class="sxs-lookup"><span data-stu-id="498df-127">The fully qualified path to the script file appears in a tooltip.</span></span>

### <a name="to-run-a-script"></a><span data-ttu-id="498df-128">Spustit skript</span><span class="sxs-lookup"><span data-stu-id="498df-128">To run a script</span></span>

<span data-ttu-id="498df-129">Na panelu nástrojů klikněte na tlačítko **spustit skript**, nebo **souboru** nabídky, klikněte na tlačítko **spustit**.</span><span class="sxs-lookup"><span data-stu-id="498df-129">On the toolbar, click **Run Script**, or on the **File** menu, click **Run**.</span></span>

### <a name="to-run-a-portion-of-a-script"></a><span data-ttu-id="498df-130">Chcete-li spustit část skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-130">To run a portion of a script</span></span>

1. <span data-ttu-id="498df-131">V podokně skriptu vyberte část skriptu.</span><span class="sxs-lookup"><span data-stu-id="498df-131">In the Script Pane, select a portion of a script.</span></span>
2. <span data-ttu-id="498df-132">Na **souboru** nabídky, klikněte na tlačítko **spustit výběr**, nebo na panelu nástrojů klikněte na tlačítko **spustit výběr**.</span><span class="sxs-lookup"><span data-stu-id="498df-132">On the **File** menu, click **Run Selection**, or on the toolbar, click **Run Selection**.</span></span>

### <a name="to-stop-a-running-script"></a><span data-ttu-id="498df-133">Chcete-li zastavit spouštění skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-133">To stop a running script</span></span>

<span data-ttu-id="498df-134">Existuje několik způsobů, jak zastavit spouštění skriptu.</span><span class="sxs-lookup"><span data-stu-id="498df-134">There are several ways to stop a running script.</span></span>

- <span data-ttu-id="498df-135">Klikněte na tlačítko **zastavení operace** na panelu nástrojů</span><span class="sxs-lookup"><span data-stu-id="498df-135">Click **Stop Operation** on the toolbar</span></span>
- <span data-ttu-id="498df-136">Stiskněte kombinaci kláves CTRL + BREAK</span><span class="sxs-lookup"><span data-stu-id="498df-136">Press CTRL+BREAK</span></span>
- <span data-ttu-id="498df-137">Vyberte **souboru** nabídky a klikněte na tlačítko **zastavení operace**.</span><span class="sxs-lookup"><span data-stu-id="498df-137">Select the **File** menu and click **Stop Operation**.</span></span>

<span data-ttu-id="498df-138">Stisknutím klávesy **CTRL + C** funguje i pokud některé je aktuálně vybraný text, v takovém případě **CTRL + C** mapuje na funkci kopírování pro vybraný text.</span><span class="sxs-lookup"><span data-stu-id="498df-138">Pressing **CTRL+C** also works unless some text is currently selected, in which case **CTRL+C** maps to the copy function for the selected text.</span></span>

## <a name="how-to-write-and-edit-text-in-the-script-pane"></a><span data-ttu-id="498df-139">Psání a upravit text z podokna skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-139">How to write and edit text in the Script Pane</span></span>

<span data-ttu-id="498df-140">Můžete zkopírovat, Vyjmout, vložit, najít a nahradit text v podokně skriptu.</span><span class="sxs-lookup"><span data-stu-id="498df-140">You can copy, cut, paste, find, and replace text in the Script Pane.</span></span> <span data-ttu-id="498df-141">Můžete také vrátit zpět a znovu provést poslední akci, kterou jste právě provedli.</span><span class="sxs-lookup"><span data-stu-id="498df-141">You can also undo and redo the last action you just performed.</span></span> <span data-ttu-id="498df-142">Klávesové zkratky pro tyto akce jsou stejné klávesové zkratky používá pro všechny aplikace Windows.</span><span class="sxs-lookup"><span data-stu-id="498df-142">The keyboard shortcuts for these actions are the same shortcuts used for all Windows applications.</span></span>

### <a name="to-enter-text-in-the-script-pane"></a><span data-ttu-id="498df-143">Zadání textu z podokna skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-143">To enter text in the Script Pane</span></span>

1. <span data-ttu-id="498df-144">Přesunutí kurzoru v podokně skriptu kliknutím na libovolné místo v podokně skriptu, nebo kliknutím **přejděte do podokna skriptu** v **zobrazení** nabídky.</span><span class="sxs-lookup"><span data-stu-id="498df-144">Move the cursor to the Script Pane by clicking anywhere in the Script Pane, or by clicking **Go to Script Pane** in the **View** menu.</span></span>
2. <span data-ttu-id="498df-145">Vytvořte skript.</span><span class="sxs-lookup"><span data-stu-id="498df-145">Create a script.</span></span> <span data-ttu-id="498df-146">Barevné zvýrazňování syntaxe a dokončování pomocí tabulátoru poskytnout bohatší možnosti úprav v prostředí Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="498df-146">Syntax coloring and tab completion provide a richer editing experience in Windows PowerShell ISE.</span></span>
3. <span data-ttu-id="498df-147">Zobrazit [postupy použití Tab k dokončování příkazů ve skriptovacím podokně a podokně konzoly](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) podrobné informace o použití funkce dokončování kartu na pomoc při psaní.</span><span class="sxs-lookup"><span data-stu-id="498df-147">See [How to Use Tab Completion in the Script Pane and Console Pane](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) for details about using the tab completion feature to help in typing.</span></span>

### <a name="to-find-text-in-the-script-pane"></a><span data-ttu-id="498df-148">Hledání textu v podokně skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-148">To find text in the Script Pane</span></span>

1. <span data-ttu-id="498df-149">Chcete-li vyhledat text kdekoli, stiskněte **CTRL + F** nebo na **upravit** nabídky, klikněte na tlačítko **najít ve skriptu**.</span><span class="sxs-lookup"><span data-stu-id="498df-149">To find text anywhere, press **CTRL+F** or, on the **Edit** menu, click **Find in Script**.</span></span>
2. <span data-ttu-id="498df-150">Hledání v textu od kurzoru, stiskněte klávesu **F3** nebo na **upravit** nabídky, klikněte na tlačítko **najít další ve skriptu**.</span><span class="sxs-lookup"><span data-stu-id="498df-150">To find text after the cursor, press **F3** or, on the **Edit** menu, click **Find Next in Script**.</span></span>
3. <span data-ttu-id="498df-151">Hledání v textu před kurzor, stiskněte klávesu **SHIFT + F3** nebo na **upravit** nabídky, klikněte na tlačítko **najít předchozí ve skriptu**.</span><span class="sxs-lookup"><span data-stu-id="498df-151">To find text before the cursor, press **SHIFT+F3** or, on the **Edit** menu, click **Find Previous in Script**.</span></span>

### <a name="to-find-and-replace-text-in-the-script-pane"></a><span data-ttu-id="498df-152">Najít a nahradit text z podokna skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-152">To find and replace text in the Script Pane</span></span>

<span data-ttu-id="498df-153">Stisknutím klávesy **CTRL + H** nebo na **upravit** nabídky, klikněte na tlačítko **nahraďte ve skriptu**.</span><span class="sxs-lookup"><span data-stu-id="498df-153">Press **CTRL+H** or, on the **Edit** menu, click **Replace in Script**.</span></span> <span data-ttu-id="498df-154">Zadejte text, který má k hledání a Nahrazovací text, stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="498df-154">Enter the text you want to find and the replacement text, then press **ENTER**.</span></span>

### <a name="to-go-to-a-particular-line-of-text-in-the-script-pane"></a><span data-ttu-id="498df-155">Chcete-li přejít na konkrétní řádek textu z podokna skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-155">To go to a particular line of text in the Script Pane</span></span>

1. <span data-ttu-id="498df-156">V podokně skriptu stisknutím klávesy **CTRL + G** nebo na **upravit** nabídky, klikněte na tlačítko **přejít na řádek**.</span><span class="sxs-lookup"><span data-stu-id="498df-156">In the Script Pane, press **CTRL+G** or, on the **Edit** menu, click **Go to Line**.</span></span>

2. <span data-ttu-id="498df-157">Zadejte číslo řádku.</span><span class="sxs-lookup"><span data-stu-id="498df-157">Enter a line number.</span></span>

### <a name="to-copy-text-in-the-script-pane"></a><span data-ttu-id="498df-158">Zkopírujte text z podokna skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-158">To copy text in the Script Pane</span></span>

1. <span data-ttu-id="498df-159">V podokně skriptu vyberte text, který chcete zkopírovat.</span><span class="sxs-lookup"><span data-stu-id="498df-159">In the Script Pane, select the text that you want to copy.</span></span>

2. <span data-ttu-id="498df-160">Stisknutím klávesy **CTRL + C** nebo na panelu nástrojů klikněte na tlačítko **kopírování** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **kopírování**.</span><span class="sxs-lookup"><span data-stu-id="498df-160">Press **CTRL+C** or, on the toolbar, click the **Copy** icon, or on the **Edit** menu, click **Copy**.</span></span>

### <a name="to-cut-text-in-the-script-pane"></a><span data-ttu-id="498df-161">Vyjmout text z podokna skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-161">To cut text in the Script Pane</span></span>

1. <span data-ttu-id="498df-162">V podokně skriptu vyberte text, který chcete vyjmout.</span><span class="sxs-lookup"><span data-stu-id="498df-162">In the Script Pane, select the text that you want to cut.</span></span>
2. <span data-ttu-id="498df-163">Stisknutím klávesy **CTRL + X** nebo na panelu nástrojů klikněte na tlačítko **Vyjmout** ikonu, nebo **upravit** nabídky, klikněte na tlačítko **Vyjmout**.</span><span class="sxs-lookup"><span data-stu-id="498df-163">Press **CTRL+X** or, on the toolbar, click the **Cut** icon, or on the **Edit** menu, click **Cut**.</span></span>

### <a name="to-paste-text-into-the-script-pane"></a><span data-ttu-id="498df-164">Vložte text do podokno skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-164">To paste text into the Script Pane</span></span>

<span data-ttu-id="498df-165">Stisknutím klávesy **CTRL + V** nebo na panelu nástrojů klikněte na tlačítko **vložit** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **vložit**.</span><span class="sxs-lookup"><span data-stu-id="498df-165">Press **CTRL+V** or, on the toolbar, click the **Paste** icon, or on the **Edit** menu, click **Paste**.</span></span>

### <a name="to-undo-an-action-in-the-script-pane"></a><span data-ttu-id="498df-166">Vrátit zpět akci z podokna skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-166">To undo an action in the Script Pane</span></span>

<span data-ttu-id="498df-167">Stisknutím klávesy **CTRL + Z** nebo na panelu nástrojů klikněte na tlačítko **zpět** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **zpět**.</span><span class="sxs-lookup"><span data-stu-id="498df-167">Press **CTRL+Z** or, on the toolbar, click the **Undo** icon, or on the **Edit** menu, click **Undo**.</span></span>

### <a name="to-redo-an-action-in-the-script-pane"></a><span data-ttu-id="498df-168">Opakování akce z podokna skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-168">To redo an action in the Script Pane</span></span>

<span data-ttu-id="498df-169">Stisknutím klávesy **CTRL + Y** nebo na panelu nástrojů klikněte na tlačítko **znovu** ikonu, nebo **upravit** nabídky, klikněte na tlačítko **znovu**.</span><span class="sxs-lookup"><span data-stu-id="498df-169">Press **CTRL+Y** or, on the toolbar, click the **Redo** icon, or on the **Edit** menu, click **Redo**.</span></span>

## <a name="how-to-save-a-script"></a><span data-ttu-id="498df-170">Uložení skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-170">How to save a script</span></span>

<span data-ttu-id="498df-171">Hvězdičku vedle názvu skriptu k označení souborů, který dosud nebyl uložen, protože se změnil.</span><span class="sxs-lookup"><span data-stu-id="498df-171">An asterisk appears next to the script name to mark a file that hasn't been saved since it was changed.</span></span> <span data-ttu-id="498df-172">Hvězdička zmizí při uložení souboru.</span><span class="sxs-lookup"><span data-stu-id="498df-172">The asterisk disappears when the file is saved.</span></span>

### <a name="to-save-a-script"></a><span data-ttu-id="498df-173">Uložte skript</span><span class="sxs-lookup"><span data-stu-id="498df-173">To save a script</span></span>

<span data-ttu-id="498df-174">Stisknutím klávesy **CTRL + S** nebo na panelu nástrojů klikněte na tlačítko **Uložit** ikonu, nebo na **souboru** nabídky, klikněte na tlačítko **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="498df-174">Press **CTRL+S** or, on the toolbar, click the **Save** icon, or on the **File** menu, click **Save**.</span></span>

### <a name="to-save-and-name-a-script"></a><span data-ttu-id="498df-175">Uložte a název skriptu</span><span class="sxs-lookup"><span data-stu-id="498df-175">To save and name a script</span></span>

1. <span data-ttu-id="498df-176">Na **souboru** nabídky, klikněte na tlačítko **uložit jako**.</span><span class="sxs-lookup"><span data-stu-id="498df-176">On the **File** menu, click **Save As**.</span></span> <span data-ttu-id="498df-177">**Uložit jako** se zobrazí dialogové okno.</span><span class="sxs-lookup"><span data-stu-id="498df-177">The **Save As** dialog box will appear.</span></span>
2. <span data-ttu-id="498df-178">V **název_souboru** pole, zadejte název souboru.</span><span class="sxs-lookup"><span data-stu-id="498df-178">In the **File name** box, enter a name for the file.</span></span>
3. <span data-ttu-id="498df-179">V **uložit jako typ** , vyberte typ souboru.</span><span class="sxs-lookup"><span data-stu-id="498df-179">In the **Save as type** box, select a file type.</span></span> <span data-ttu-id="498df-180">Například v **uložit jako typ** vyberte "skriptů Powershellu (\*.ps1)".</span><span class="sxs-lookup"><span data-stu-id="498df-180">For example, in the **Save as type** box, select 'PowerShell Scripts (\*.ps1)'.</span></span>
4. <span data-ttu-id="498df-181">Klikněte na **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="498df-181">Click **Save**.</span></span>

### <a name="to-save-a-script-in-ascii-encoding"></a><span data-ttu-id="498df-182">Uložte skript v kódování ASCII</span><span class="sxs-lookup"><span data-stu-id="498df-182">To save a script in ASCII encoding</span></span>

<span data-ttu-id="498df-183">Ve výchozím nastavení Windows PowerShell ISE uloží nové soubory skriptu (.ps1), datové soubory skriptu (.psd1) a soubory modulu skriptu (.psm1) jako kódování Unicode (BigEndianUnicode) ve výchozím nastavení. Některá uložit skript v jiné kódování, jako je například ASCII (ANSI), použijte **Uložit** nebo **SaveAs** metody [$psISE.CurrentFile](the-ise-object-model-hierarchy.md) objektu.</span><span class="sxs-lookup"><span data-stu-id="498df-183">By default, Windows PowerShell ISE saves new script files (.ps1), script data files (.psd1), and script module files (.psm1) as Unicode (BigEndianUnicode) by default.Â To save a script in another encoding, such as ASCII (ANSI), use the **Save** or **SaveAs** methods on the [$psISE.CurrentFile](the-ise-object-model-hierarchy.md) object.</span></span>

<span data-ttu-id="498df-184">Následující příkaz uloží nový skript jako MyScript.ps1 s kódováním ASCII.</span><span class="sxs-lookup"><span data-stu-id="498df-184">The following command saves a new script as MyScript.ps1 with ASCII encoding.</span></span>

```powershell
$psISE.CurrentFile.SaveAs("MyScript.ps1", [System.Text.Encoding]::ASCII)
```

<span data-ttu-id="498df-185">Následující příkaz nahradí aktuální soubor skriptu se souborem se stejným názvem, ale s kódováním ASCII.</span><span class="sxs-lookup"><span data-stu-id="498df-185">The following command replaces the current script file with a file with the same name, but with ASCII encoding.</span></span>

```powershell
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)
```

<span data-ttu-id="498df-186">V následujícím příkazu je získán kódování aktuálního souboru.</span><span class="sxs-lookup"><span data-stu-id="498df-186">The following command gets the encoding of the current file.</span></span>

```powershell
$psISE.CurrentFile.encoding
```

<span data-ttu-id="498df-187">Windows PowerShell ISE podporuje následující možnosti kódování: ASCII, BigEndianUnicode, Unicode, UTF32, UTF7, UTF8 a výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="498df-187">Windows PowerShell ISE supports the following encoding options: ASCII, BigEndianUnicode, Unicode, UTF32, UTF7, UTF8, and Default.</span></span> <span data-ttu-id="498df-188">Hodnotu výchozí možnosti se liší podle systému.</span><span class="sxs-lookup"><span data-stu-id="498df-188">The value of the Default option varies with the system.</span></span>

<span data-ttu-id="498df-189">Windows PowerShell ISE nedojde ke změně kódování souborů skriptu, použijete-li uložit nebo uložit jako příkazy.</span><span class="sxs-lookup"><span data-stu-id="498df-189">Windows PowerShell ISE doesn't change the encoding of script files when you use the Save or Save As commands.</span></span>

## <a name="see-also"></a><span data-ttu-id="498df-190">Viz také</span><span class="sxs-lookup"><span data-stu-id="498df-190">See Also</span></span>

- [<span data-ttu-id="498df-191">Seznámení s prostředím Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="498df-191">Exploring the Windows PowerShell ISE</span></span>](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
