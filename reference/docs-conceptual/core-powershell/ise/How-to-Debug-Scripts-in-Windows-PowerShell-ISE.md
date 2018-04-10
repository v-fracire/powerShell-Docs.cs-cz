---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Ladění skriptů v prostředí Windows PowerShell ISE
ms.openlocfilehash: b7af2de83a3f796a2057514e36ad8b74367e8ce2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="how-to-debug-scripts-in-windows-powershell-ise"></a><span data-ttu-id="78640-103">Ladění skriptů v prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="78640-103">How to Debug Scripts in Windows PowerShell ISE</span></span>

<span data-ttu-id="78640-104">Tento článek popisuje postup ladění skriptů v místním počítači pomocí funkce Windows PowerShell Integrované skriptovací prostředí (ISE) visual ladění.</span><span class="sxs-lookup"><span data-stu-id="78640-104">This article describes how to debug scripts on a local computer by using the Windows PowerShell Integrated Scripting Environment (ISE) visual debugging features.</span></span>

## <a name="how-to-manage-breakpoints"></a><span data-ttu-id="78640-105">Jak spravovat zarážky</span><span class="sxs-lookup"><span data-stu-id="78640-105">How to manage breakpoints</span></span>

<span data-ttu-id="78640-106">Zarážka je určené místo ve skriptu, kam chcete operaci pozastavit, takže můžete zkontrolovat aktuální stav proměnné a prostředí, ve kterém běží váš skript.</span><span class="sxs-lookup"><span data-stu-id="78640-106">A breakpoint is a designated spot in a script where you would like operation to pause so that you can examine the current state of the variables and the environment in which your script is running.</span></span> <span data-ttu-id="78640-107">Jakmile vašeho skriptu je pozastaveno boru přerušení, můžete spustit příkazy v podokně konzole zkontrolujte stav vašeho skriptu.</span><span class="sxs-lookup"><span data-stu-id="78640-107">Once your script is paused by a breakpoint, you can run commands in the Console Pane to examine the state of your script.</span></span>  <span data-ttu-id="78640-108">Můžete výstup proměnné nebo spouštění jiných příkazů.</span><span class="sxs-lookup"><span data-stu-id="78640-108">You can output variables or run other commands.</span></span> <span data-ttu-id="78640-109">Dokonce můžete upravit hodnotu proměnných, které jsou viditelné pro kontext probíhající skriptu.</span><span class="sxs-lookup"><span data-stu-id="78640-109">You can even modify the value of any variables that are visible to the context of the currently running script.</span></span> <span data-ttu-id="78640-110">Po zkontrolují co chcete zobrazit můžete obnovit operace skriptu.</span><span class="sxs-lookup"><span data-stu-id="78640-110">After you have examined what you want to see, you can resume operation of the script.</span></span>

<span data-ttu-id="78640-111">Tři typy zarážky můžete nastavit v ladění prostředí Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="78640-111">You can set three types of breakpoints in the Windows PowerShell debugging environment:</span></span>

1. <span data-ttu-id="78640-112">**Řádek zarážek**.</span><span class="sxs-lookup"><span data-stu-id="78640-112">**Line breakpoint**.</span></span> <span data-ttu-id="78640-113">Skript se pozastaví po dosažení určené řádku během operace skriptu</span><span class="sxs-lookup"><span data-stu-id="78640-113">The script pauses when the designated line is reached during the operation of the script</span></span>

2. <span data-ttu-id="78640-114">**Proměnné zarážek.**</span><span class="sxs-lookup"><span data-stu-id="78640-114">**Variable breakpoint.**</span></span> <span data-ttu-id="78640-115">Skript pozastaví při každé změně hodnoty proměnné určené.</span><span class="sxs-lookup"><span data-stu-id="78640-115">The script pauses whenever the designated variable's value changes.</span></span>

3. <span data-ttu-id="78640-116">**Příkaz zarážek.**</span><span class="sxs-lookup"><span data-stu-id="78640-116">**Command breakpoint.**</span></span> <span data-ttu-id="78640-117">Skript pozastaví vždy, když je určený příkaz bude během operace skript spuštěný.</span><span class="sxs-lookup"><span data-stu-id="78640-117">The script pauses whenever the designated command is about to be run during the operation of the script.</span></span> <span data-ttu-id="78640-118">Může obsahovat parametry pro další filtrování zarážek pouze operace, které chcete.</span><span class="sxs-lookup"><span data-stu-id="78640-118">It can include parameters to further filter the breakpoint to only the operation you want.</span></span> <span data-ttu-id="78640-119">Příkaz může být také funkci, kterou jste vytvořili.</span><span class="sxs-lookup"><span data-stu-id="78640-119">The command can also be a function you created.</span></span>

<span data-ttu-id="78640-120">Z těchto v prostředí Windows PowerShell ISE ladění lze nastavit pouze řádku zarážky pomocí nabídky nebo klávesové zkratky.</span><span class="sxs-lookup"><span data-stu-id="78640-120">Of these, in the Windows PowerShell ISE debugging environment, only line breakpoints can be set by using the menu or the keyboard shortcuts.</span></span> <span data-ttu-id="78640-121">Další dva typy zarážky lze nastavit, ale jsou nastavené v podokně konzoly pomocí [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) rutiny.</span><span class="sxs-lookup"><span data-stu-id="78640-121">The other two types of breakpoints can be set, but they are set from the Console Pane by using the [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) cmdlet.</span></span> <span data-ttu-id="78640-122">Tato část popisuje, jak můžete provádět ladění úkoly v systému Windows PowerShell ISE pomocí nabídek, pokud je k dispozici a provádět širší rozsah příkazy z podokna konzoly pomocí skriptování.</span><span class="sxs-lookup"><span data-stu-id="78640-122">This section describes how you can perform debugging tasks in Windows PowerShell ISE by using the menus where available, and perform a wider range of commands from the Console Pane by using scripting.</span></span>

### <a name="to-set-a-breakpoint"></a><span data-ttu-id="78640-123">Chcete-li nastavit zarážky</span><span class="sxs-lookup"><span data-stu-id="78640-123">To set a breakpoint</span></span>

<span data-ttu-id="78640-124">Ve skriptu můžete nastavit zarážky, až poté, co byl uložen.</span><span class="sxs-lookup"><span data-stu-id="78640-124">A breakpoint can be set in a script only after it has been saved.</span></span> <span data-ttu-id="78640-125">Klikněte pravým tlačítkem na řádek, ve které chcete nastavit zarážky řádku a potom klikněte na **Přepnout zarážku**.</span><span class="sxs-lookup"><span data-stu-id="78640-125">Right-click the line where you want to set a line breakpoint, and then click **Toggle Breakpoint**.</span></span> <span data-ttu-id="78640-126">Nebo klikněte na řádek, ve které chcete nastavit zarážky řádek, a stiskněte klávesu **F9** nebo na **ladění** nabídky, klikněte na tlačítko **Přepnout zarážku**.</span><span class="sxs-lookup"><span data-stu-id="78640-126">Or, click the line where you want to set a line breakpoint, and press **F9** or, on the **Debug** menu, click **Toggle Breakpoint**.</span></span>

<span data-ttu-id="78640-127">Následující skript je příklad, jak můžete nastavit proměnné zarážek v podokně konzoly pomocí [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) rutiny.</span><span class="sxs-lookup"><span data-stu-id="78640-127">The following script is an example of how you can set a variable breakpoint from the Console Pane by using the [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) cmdlet.</span></span>

```powershell
# This command sets a breakpoint on the Server variable in the Sample.ps1 script.
Set-PSBreakpoint -Script sample.ps1 -Variable Server
```

### <a name="list-all-breakpoints"></a><span data-ttu-id="78640-128">Zobrazí seznam všech zarážky</span><span class="sxs-lookup"><span data-stu-id="78640-128">List all breakpoints</span></span>

<span data-ttu-id="78640-129">Zobrazí všechny zarážky v aktuální relaci prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78640-129">Displays all breakpoints in the current Windows PowerShell session.</span></span>

<span data-ttu-id="78640-130">Na **ladění** nabídky, klikněte na tlačítko **seznamu zarážky**.</span><span class="sxs-lookup"><span data-stu-id="78640-130">On the **Debug** menu, click **List Breakpoints**.</span></span> <span data-ttu-id="78640-131">Následující skript je příklad, jak můžete vytvořit seznam všech zarážky z podokna konzoly pomocí [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) rutiny.</span><span class="sxs-lookup"><span data-stu-id="78640-131">The following script is an example of how you can list all breakpoints from the Console Pane by using the [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) cmdlet.</span></span>

```powershell
# This command lists all breakpoints in the current session.
Get-PSBreakpoint
```

### <a name="remove-a-breakpoint"></a><span data-ttu-id="78640-132">Odstranění zarážky</span><span class="sxs-lookup"><span data-stu-id="78640-132">Remove a breakpoint</span></span>

<span data-ttu-id="78640-133">Odebrání zarážku neodstraní.</span><span class="sxs-lookup"><span data-stu-id="78640-133">Removing a breakpoint deletes it.</span></span>

<span data-ttu-id="78640-134">Pokud se domníváte, že budete chtít pozdější použití, zvažte [zakázat zarážku](#disable-a-breakpoint) ho místo.</span><span class="sxs-lookup"><span data-stu-id="78640-134">If you think you might want to use it again later, consider [Disable a Breakpoint](#disable-a-breakpoint) it instead.</span></span>
<span data-ttu-id="78640-135">Klikněte pravým tlačítkem na řádek, ve které chcete odebrat bod přerušení a potom klikněte na **Přepnout zarážku**.</span><span class="sxs-lookup"><span data-stu-id="78640-135">Right-click the line where you want to remove a breakpoint, and then click **Toggle Breakpoint**.</span></span>
<span data-ttu-id="78640-136">Nebo klikněte na řádek, ve které chcete odebrat bod přerušení, a na **ladění** nabídky, klikněte na tlačítko **Přepnout zarážku**.</span><span class="sxs-lookup"><span data-stu-id="78640-136">Or, click the line where you want to remove a breakpoint, and on the **Debug** menu, click **Toggle Breakpoint**.</span></span>
<span data-ttu-id="78640-137">Následující skript představuje příklad, jak odebrat zarážku se zadaným ID z podokna konzoly pomocí [odebrat PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) rutiny.</span><span class="sxs-lookup"><span data-stu-id="78640-137">The following script is an example of how to remove a breakpoint with a specified ID from the Console Pane by using the [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet.</span></span>

```powershell
# This command deletes the breakpoint with breakpoint ID 2.
Remove-PSBreakpoint -Id 2
```

### <a name="remove-all-breakpoints"></a><span data-ttu-id="78640-138">Odeberte všechny zarážky</span><span class="sxs-lookup"><span data-stu-id="78640-138">Remove All Breakpoints</span></span>

<span data-ttu-id="78640-139">Chcete-li odebrat všechny zarážky definované v aktuální relaci, na **ladění** nabídky, klikněte na tlačítko **odebrat všechny zarážky**.</span><span class="sxs-lookup"><span data-stu-id="78640-139">To remove all breakpoints defined in the current session, on the **Debug** menu, click **Remove All Breakpoints**.</span></span>

<span data-ttu-id="78640-140">Následující skript představuje příklad, jak odebrat všechny zarážky v podokně konzoly pomocí [odebrat PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) rutiny.</span><span class="sxs-lookup"><span data-stu-id="78640-140">The following script is an example of how to remove all breakpoints from the Console Pane by using the [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet.</span></span>

```powershell
# This command deletes all of the breakpoints in the current session.
Get-PSBreakpoint | Remove-PSBreakpoint
```

### <a name="disable-a-breakpoint"></a><span data-ttu-id="78640-141">Zakázat zarážky</span><span class="sxs-lookup"><span data-stu-id="78640-141">Disable a Breakpoint</span></span>

<span data-ttu-id="78640-142">Zakázání zarážku neodebere. ji vypne dokud není povoleno.</span><span class="sxs-lookup"><span data-stu-id="78640-142">Disabling a breakpoint does not remove it; it turns it off until it is enabled.</span></span>  <span data-ttu-id="78640-143">Zakázat zarážku konkrétní řádku, klikněte pravým tlačítkem na řádek, kde chcete zakázat zarážku, a pak klikněte na **zakázat zarážek**.</span><span class="sxs-lookup"><span data-stu-id="78640-143">To disable a specific line breakpoint, right-click the line where you want to disable a breakpoint, and then click **Disable Breakpoint**.</span></span> <span data-ttu-id="78640-144">Nebo klikněte na řádek, ve které chcete zakázat zarážku, a stiskněte klávesu **F9** nebo na **ladění** nabídky, klikněte na tlačítko **zakázat zarážek**.</span><span class="sxs-lookup"><span data-stu-id="78640-144">Or, click the line where you want to disable a breakpoint, and press **F9** or, on the **Debug** menu, click **Disable Breakpoint**.</span></span> <span data-ttu-id="78640-145">Následující skript je příklad odebrání zarážek se zadaným ID z podokna konzoly pomocí [zakázat PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) rutiny.</span><span class="sxs-lookup"><span data-stu-id="78640-145">The following script is an example of how you can remove a breakpoint with a specified ID from the Console Pane by using the [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet.</span></span>

```powershell
# This command disables the breakpoint with breakpoint ID 0.
Disable-PSBreakpoint -Id 0
```

### <a name="disable-all-breakpoints"></a><span data-ttu-id="78640-146">Zakažte všechny zarážky</span><span class="sxs-lookup"><span data-stu-id="78640-146">Disable All Breakpoints</span></span>

<span data-ttu-id="78640-147">Zakázání zarážku neodebere. ji vypne dokud není povoleno.</span><span class="sxs-lookup"><span data-stu-id="78640-147">Disabling a breakpoint does not remove it; it turns it off until it is enabled.</span></span>  <span data-ttu-id="78640-148">Zakázání všechny zarážky v aktuální relaci, na **ladění** nabídky, klikněte na tlačítko **zakažte všechny zarážky**.</span><span class="sxs-lookup"><span data-stu-id="78640-148">To disable all breakpoints in the current session, on the **Debug** menu, click **Disable all Breakpoints**.</span></span> <span data-ttu-id="78640-149">Následující skript je příklad, jak můžete zakázat všechna zarážky z podokna konzoly pomocí [zakázat PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) rutiny.</span><span class="sxs-lookup"><span data-stu-id="78640-149">The following script is an example of how you can disable all breakpoints from the Console Pane by using the [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet.</span></span>

```powershell
# This command disables all breakpoints in the current session.
# You can abbreviate this command as: "gbp | dbp".
Get-PSBreakpoint | Disable-PSBreakpoint
```

### <a name="enable-a-breakpoint"></a><span data-ttu-id="78640-150">Povolit zarážky</span><span class="sxs-lookup"><span data-stu-id="78640-150">Enable a Breakpoint</span></span>

<span data-ttu-id="78640-151">Pokud chcete povolit konkrétní zarážek, klikněte pravým tlačítkem na řádek, ve které chcete povolit zarážku a pak klikněte na **povolit zarážek**.</span><span class="sxs-lookup"><span data-stu-id="78640-151">To enable a specific breakpoint, right-click the line where you want to enable a breakpoint, and then click **Enable Breakpoint**.</span></span> <span data-ttu-id="78640-152">Nebo klikněte na řádek, kde chcete povolit zarážky, a potom stiskněte klávesu **F9** nebo na **ladění** nabídky, klikněte na tlačítko **povolit zarážek**.</span><span class="sxs-lookup"><span data-stu-id="78640-152">Or, click the line where you want to enable a breakpoint, and then press **F9** or, on the **Debug** menu, click **Enable Breakpoint**.</span></span> <span data-ttu-id="78640-153">Následující skript je příklad, jak můžete povolit konkrétní zarážky z podokna konzoly pomocí [povolit PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) rutiny.</span><span class="sxs-lookup"><span data-stu-id="78640-153">The following script is an example of how you can enable specific breakpoints from the Console Pane by using the [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet.</span></span>

```powershell
# This command enables breakpoints with breakpoint IDs 0, 1, and 5.
Enable-PSBreakpoint -Id 0, 1, 5
```

### <a name="enable-all-breakpoints"></a><span data-ttu-id="78640-154">Povolit všechny zarážky</span><span class="sxs-lookup"><span data-stu-id="78640-154">Enable All Breakpoints</span></span>

<span data-ttu-id="78640-155">Povolit všechny zarážky definované v aktuální relaci, na **ladění** nabídky, klikněte na tlačítko **povolit všechny zarážky**.</span><span class="sxs-lookup"><span data-stu-id="78640-155">To enable all breakpoints defined in the current session, on the **Debug** menu, click **Enable all Breakpoints**.</span></span> <span data-ttu-id="78640-156">Následující skript je příklad, jak můžete povolit všechny zarážky v podokně konzoly pomocí [povolit PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) rutiny.</span><span class="sxs-lookup"><span data-stu-id="78640-156">The following script is an example of how you can enable all breakpoints from the Console Pane by using the [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet.</span></span>

```powershell
# This command enables all breakpoints in the current session.
# You can abbreviate the command by using their aliases: "gbp | ebp".
Get-PSBreakpoint | Enable-PSBreakpoint
```

## <a name="how-to-manage-a-debugging-session"></a><span data-ttu-id="78640-157">Jak spravovat ladicí relace</span><span class="sxs-lookup"><span data-stu-id="78640-157">How to manage a debugging session</span></span>

<span data-ttu-id="78640-158">Než začnete, ladění, musíte nastavit jeden nebo více zarážky.</span><span class="sxs-lookup"><span data-stu-id="78640-158">Before you start debugging, you must set one or more breakpoints.</span></span> <span data-ttu-id="78640-159">Zarážku nelze nastavit, pokud je uložen skript, který chcete ladit.</span><span class="sxs-lookup"><span data-stu-id="78640-159">You cannot set a breakpoint unless the script that you want to debug is saved.</span></span> <span data-ttu-id="78640-160">Pokyny o tom, jak nastavit zarážky, najdete v části [Správa zarážky](#how-to-manage-breakpoints) nebo [Set-PSBreakpoint](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/set-psbreakpoint).</span><span class="sxs-lookup"><span data-stu-id="78640-160">For directions on of how to set a breakpoint, see [How to manage breakpoints](#how-to-manage-breakpoints) or [Set-PSBreakpoint](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/set-psbreakpoint).</span></span> <span data-ttu-id="78640-161">Po spuštění ladění, nelze upravit skript, dokud jej nezastavíte ladění.</span><span class="sxs-lookup"><span data-stu-id="78640-161">After you start debugging, you cannot edit a script until you stop debugging.</span></span> <span data-ttu-id="78640-162">Skript, který má jeden nebo více zarážky nastavit je automaticky uloží, než je spuštěn.</span><span class="sxs-lookup"><span data-stu-id="78640-162">A script that has one or more breakpoints set is automatically saved before it is run.</span></span>

### <a name="to-start-debugging"></a><span data-ttu-id="78640-163">Spustit ladění</span><span class="sxs-lookup"><span data-stu-id="78640-163">To start debugging</span></span>

<span data-ttu-id="78640-164">Stiskněte klávesu **F5** nebo na panelu nástrojů klikněte na tlačítko **spustit skript** ikonu, nebo na **ladění** nabídce klikněte na tlačítko **spustit nebo pokračovat**.</span><span class="sxs-lookup"><span data-stu-id="78640-164">Press **F5** or, on the toolbar, click the **Run Script** icon, or on the **Debug** menu click **Run/Continue**.</span></span> <span data-ttu-id="78640-165">Skript se spustí, dokud zjistí první zarážky.</span><span class="sxs-lookup"><span data-stu-id="78640-165">The script runs until it encounters the first breakpoint.</span></span> <span data-ttu-id="78640-166">To pozastaví operaci tam a klade důraz na řádku, na kterém je pozastavena.</span><span class="sxs-lookup"><span data-stu-id="78640-166">It pauses operation there and highlights the line on which it paused.</span></span>

### <a name="to-continue-debugging"></a><span data-ttu-id="78640-167">Chcete-li pokračovat, ladění</span><span class="sxs-lookup"><span data-stu-id="78640-167">To continue debugging</span></span>

<span data-ttu-id="78640-168">Stiskněte klávesu **F5** nebo na panelu nástrojů klikněte na tlačítko **spustit skript** ikonu, nebo na **ladění** nabídky, klikněte na tlačítko **spustit nebo pokračovat** nebo v podokně konzoly, zadejte **C** a potom stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="78640-168">Press **F5** or, on the toolbar, click the **Run Script** icon, or on the **Debug** menu, click **Run/Continue** or, in the Console Pane, type **C** and then press **ENTER**.</span></span> <span data-ttu-id="78640-169">To způsobí, že skript, který chcete-li pokračovat v provozu na další zarážku nebo na konec skriptu, pokud nedojde k žádné další zarážky.</span><span class="sxs-lookup"><span data-stu-id="78640-169">This causes the script to continue running to the next breakpoint or to the end of the script if no further breakpoints are encountered.</span></span>

### <a name="to-view-the-call-stack"></a><span data-ttu-id="78640-170">Chcete-li zobrazit zásobníku volání</span><span class="sxs-lookup"><span data-stu-id="78640-170">To view the call stack</span></span>

<span data-ttu-id="78640-171">Zásobník volání zobrazí aktuální spuštění umístění ve skriptu.</span><span class="sxs-lookup"><span data-stu-id="78640-171">The call stack displays the current run location in the script.</span></span> <span data-ttu-id="78640-172">Pokud skriptu běží ve funkci, která byla zavolána různých funkcí, pak která je reprezentována v zobrazení dodatečné řádky ve výstupu.</span><span class="sxs-lookup"><span data-stu-id="78640-172">If the script is running in a function that was called by a different function, then that is represented in the display by additional rows in the output.</span></span> <span data-ttu-id="78640-173">Spodní krajní řádek zobrazí původní skript a na řádku v ní ve kterém byla zavolána funkce.</span><span class="sxs-lookup"><span data-stu-id="78640-173">The bottom-most row displays the original script and the line in it in which a function was called.</span></span> <span data-ttu-id="78640-174">Další rovině ukazuje, že funkce a řádku v ní ve kterém může mít jinou funkci zavolání.</span><span class="sxs-lookup"><span data-stu-id="78640-174">The next line up shows that function and the line in it in which another function might have been called.</span></span>  <span data-ttu-id="78640-175">Nejvyšší řádek ukazuje aktuální kontext aktuálního řádku, na kterém je nastaven breakpoint.</span><span class="sxs-lookup"><span data-stu-id="78640-175">The top-most row shows the current context of the current line on which the breakpoint is set.</span></span>

<span data-ttu-id="78640-176">Při pozastavena, chcete-li zobrazit aktuální zásobníku volání, stiskněte **CTRL + SHIFT + D** nebo na **ladění** nabídky, klikněte na tlačítko **zásobníkem volání zobrazení** nebo v podokně konzoly zadejte **kB**  a potom stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="78640-176">While paused, to see the current call stack, press **CTRL+SHIFT+D** or, on the **Debug** menu, click **Display Call Stack** or, in the Console Pane, type **K** and then press **ENTER**.</span></span>

### <a name="to-stop-debugging"></a><span data-ttu-id="78640-177">Aby se ukončilo ladění</span><span class="sxs-lookup"><span data-stu-id="78640-177">To stop debugging</span></span>

<span data-ttu-id="78640-178">Stiskněte klávesu **SHIFT + F5** nebo na **ladění** nabídky, klikněte na tlačítko **zastavení ladicího programu**, nebo v podokně konzoly zadejte **Q** a potom stiskněte klávesu  **Zadejte**.</span><span class="sxs-lookup"><span data-stu-id="78640-178">Press **SHIFT-F5** or, on the **Debug** menu, click **Stop Debugger**, or, in the Console Pane, type **Q** and then press **ENTER**.</span></span>

## <a name="how-to-step-over-step-into-and-step-out-while-debugging"></a><span data-ttu-id="78640-179">Postup krok přes, krok do a krok při ladění</span><span class="sxs-lookup"><span data-stu-id="78640-179">How to step over, step into, and step out while debugging</span></span>

<span data-ttu-id="78640-180">Krokování je proces spuštěný jeden příkaz v čase.</span><span class="sxs-lookup"><span data-stu-id="78640-180">Stepping is the process of running one statement at a time.</span></span> <span data-ttu-id="78640-181">Můžete zastavit na řádek kódu a zkontrolujte hodnoty proměnné a stavu systému.</span><span class="sxs-lookup"><span data-stu-id="78640-181">You can stop on a line of code, and examine the values of variables and the state of the system.</span></span> <span data-ttu-id="78640-182">Následující tabulka popisuje běžné úkoly ladění jako krokování přes, zanoříte se do a zanoříte.</span><span class="sxs-lookup"><span data-stu-id="78640-182">The following table describes common debugging tasks such as stepping over, stepping into, and stepping out.</span></span>

| <span data-ttu-id="78640-183">Ladění úloh</span><span class="sxs-lookup"><span data-stu-id="78640-183">Debugging Task</span></span> | <span data-ttu-id="78640-184">Popis</span><span class="sxs-lookup"><span data-stu-id="78640-184">Description</span></span> | <span data-ttu-id="78640-185">Jak provést v prostředí PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="78640-185">How to accomplish it in PowerShell ISE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="78640-186">**Krok do**</span><span class="sxs-lookup"><span data-stu-id="78640-186">**Step Into**</span></span> | <span data-ttu-id="78640-187">Aktuální příkaz a poté se zastaví v další příkaz.</span><span class="sxs-lookup"><span data-stu-id="78640-187">Executes the current statement and then stops at the next statement.</span></span> <span data-ttu-id="78640-188">Pokud aktuální příkaz funkce nebo skriptu volání a pak ladicí program do této funkce nebo skriptu, jinak se zastaví v další příkaz.</span><span class="sxs-lookup"><span data-stu-id="78640-188">If the current statement is a function or script call, then the debugger steps into that function or script, otherwise it stops at the next statement.</span></span> | <span data-ttu-id="78640-189">Stiskněte klávesu **F11** nebo na **ladění** nabídky, klikněte na tlačítko **Krokovat s vnořením**, nebo v podokně konzoly zadejte **S** a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="78640-189">Press **F11** or, on the **Debug** menu, click **Step Into**, or in the Console Pane, type **S** and press **ENTER**.</span></span> |
| <span data-ttu-id="78640-190">**Krok přes**</span><span class="sxs-lookup"><span data-stu-id="78640-190">**Step Over**</span></span> | <span data-ttu-id="78640-191">Aktuální příkaz a poté se zastaví v další příkaz.</span><span class="sxs-lookup"><span data-stu-id="78640-191">Executes the current statement and then stops at the next statement.</span></span> <span data-ttu-id="78640-192">Pokud je aktuální příkaz funkce nebo skriptu volání a pak ladicí program provede celou funkce nebo skriptu a zastaví v další příkaz po volání funkce.</span><span class="sxs-lookup"><span data-stu-id="78640-192">If the current statement is a function or script call, then the debugger executes the whole function or script, and it stops at the next statement after the function call.</span></span> | <span data-ttu-id="78640-193">Stiskněte klávesu **F10** nebo na **ladění** nabídky, klikněte na tlačítko **Krokovat s přeskočením**, nebo v podokně konzoly zadejte **V** a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="78640-193">Press **F10** or, on the **Debug** menu, click **Step Over**, or in the Console Pane, type **V** and press **ENTER**.</span></span> |
| <span data-ttu-id="78640-194">**Krok**</span><span class="sxs-lookup"><span data-stu-id="78640-194">**Step Out**</span></span> | <span data-ttu-id="78640-195">Kroky mimo funkci current a jednu úroveň, pokud je vnořené funkce.</span><span class="sxs-lookup"><span data-stu-id="78640-195">Steps out of the current function and up one level if the function is nested.</span></span> <span data-ttu-id="78640-196">Pokud v hlavní, skript se spustí na konec nebo na další zarážku.</span><span class="sxs-lookup"><span data-stu-id="78640-196">If in the main body, the script is executed to the end, or to the next breakpoint.</span></span> <span data-ttu-id="78640-197">Bylo vynecháno příkazy jsou provést, ale není provedl.</span><span class="sxs-lookup"><span data-stu-id="78640-197">The skipped statements are executed, but not stepped through.</span></span> | <span data-ttu-id="78640-198">Stiskněte klávesu **SHIFT + F11**, nebo na **ladění** nabídky, klikněte na tlačítko **Krokovat s Vystoupením**, nebo v podokně konzoly zadejte **O** a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="78640-198">Press **SHIFT+F11**, or on the **Debug** menu, click **Step Out**, or in the Console Pane, type **O** and press **ENTER**.</span></span> |
| <span data-ttu-id="78640-199">**Pokračovat**</span><span class="sxs-lookup"><span data-stu-id="78640-199">**Continue**</span></span> | <span data-ttu-id="78640-200">Pokračuje v provádění na konec nebo na další zarážku.</span><span class="sxs-lookup"><span data-stu-id="78640-200">Continues execution to the end, or to the next breakpoint.</span></span> <span data-ttu-id="78640-201">Bylo vynecháno funkce a volání jsou provést, ale není provedl.</span><span class="sxs-lookup"><span data-stu-id="78640-201">The skipped functions and invocations are executed, but not stepped through.</span></span> | <span data-ttu-id="78640-202">Stiskněte klávesu **F5** nebo na **ladění** nabídky, klikněte na tlačítko **spustit nebo pokračovat**, nebo v podokně konzoly zadejte **C** a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="78640-202">Press **F5** or, on the **Debug** menu, click **Run/Continue**, or in the Console Pane, type **C** and press **ENTER**.</span></span> |

## <a name="how-to-display-the-values-of-variables-while-debugging"></a><span data-ttu-id="78640-203">Postupy: zobrazení hodnot proměnných při ladění</span><span class="sxs-lookup"><span data-stu-id="78640-203">How to display the values of variables while debugging</span></span>

<span data-ttu-id="78640-204">V průběhu kód můžete zobrazit aktuální hodnoty proměnné ve skriptu.</span><span class="sxs-lookup"><span data-stu-id="78640-204">You can display the current values of variables in the script as you step through the code.</span></span>

### <a name="to-display-the-values-of-standard-variables"></a><span data-ttu-id="78640-205">K zobrazení hodnot proměnných standardní</span><span class="sxs-lookup"><span data-stu-id="78640-205">To display the values of standard variables</span></span>

<span data-ttu-id="78640-206">Použijte jednu z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="78640-206">Use one of the following methods:</span></span>

- <span data-ttu-id="78640-207">V podokně skriptu pozastavte ukazatel myši nad proměnnou k zobrazení jeho hodnoty jako popis tlačítka.</span><span class="sxs-lookup"><span data-stu-id="78640-207">In the Script Pane, hover over the variable to display its value as a tool tip.</span></span>

- <span data-ttu-id="78640-208">V podokně konzoly, zadejte název proměnné a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="78640-208">In the Console Pane, type the variable name and press **ENTER**.</span></span>

<span data-ttu-id="78640-209">Všechny podokna (ISE) v jsou vždycky ve stejném oboru.</span><span class="sxs-lookup"><span data-stu-id="78640-209">All panes in ISE are always in the same scope.</span></span> <span data-ttu-id="78640-210">Proto v při ladění skriptu, spusťte příkazy, které zadáte v podokně konzoly v oboru skriptu.</span><span class="sxs-lookup"><span data-stu-id="78640-210">Therefore, while you are debugging a script, the commands that you type in the Console Pane run in script scope.</span></span> <span data-ttu-id="78640-211">To umožňuje používat k vyhledání hodnoty proměnných a volání funkce, které jsou definovány pouze ve skriptu v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="78640-211">This allows you to use the Console Pane to find the values of variables and call functions that are defined only in the script.</span></span>

### <a name="to-display-the-values-of-automatic-variables"></a><span data-ttu-id="78640-212">K zobrazení hodnot proměnných automatické</span><span class="sxs-lookup"><span data-stu-id="78640-212">To display the values of automatic variables</span></span>

<span data-ttu-id="78640-213">Předchozí postup můžete použít k zobrazení hodnot proměnných téměř všechny při ladění skriptu.</span><span class="sxs-lookup"><span data-stu-id="78640-213">You can use the preceding method to display the value of almost all variables while you are debugging a script.</span></span> <span data-ttu-id="78640-214">Tyto metody se ale nefungují pro následující automatické proměnné.</span><span class="sxs-lookup"><span data-stu-id="78640-214">However, these methods do not work for the following automatic variables.</span></span>

- <span data-ttu-id="78640-215">$_</span><span class="sxs-lookup"><span data-stu-id="78640-215">$_</span></span>

- <span data-ttu-id="78640-216">$Input</span><span class="sxs-lookup"><span data-stu-id="78640-216">$Input</span></span>

- <span data-ttu-id="78640-217">$MyInvocation</span><span class="sxs-lookup"><span data-stu-id="78640-217">$MyInvocation</span></span>

- <span data-ttu-id="78640-218">$PSBoundParameters</span><span class="sxs-lookup"><span data-stu-id="78640-218">$PSBoundParameters</span></span>

- <span data-ttu-id="78640-219">$Args</span><span class="sxs-lookup"><span data-stu-id="78640-219">$Args</span></span>

<span data-ttu-id="78640-220">Pokud se pokusíte zobrazit hodnotu tyto proměnné, můžete získat hodnotu této proměnné v interní kanálu ladicí program používá, není hodnota proměnné ve skriptu.</span><span class="sxs-lookup"><span data-stu-id="78640-220">If you try to display the value of any of these variables, you get the value of that variable for in an internal pipeline the debugger uses, not the value of the variable in the script.</span></span> <span data-ttu-id="78640-221">Můžete obejít tím pár proměnných ($_, $Input, $MyInvocation, $PSBoundParameters a $Args) pomocí následující metody:</span><span class="sxs-lookup"><span data-stu-id="78640-221">You can work around this for a few variables ($_, $Input, $MyInvocation, $PSBoundParameters, and $Args) by using the following method:</span></span>

1. <span data-ttu-id="78640-222">Ve skriptu přiřadíte hodnotu proměnné, automatické nové proměnné.</span><span class="sxs-lookup"><span data-stu-id="78640-222">In the script, assign the value of the automatic variable to a new variable.</span></span>

2. <span data-ttu-id="78640-223">Zobrazte hodnotu nové proměnné, ukázáním myší nové proměnné v podokně skriptu nebo zadáním nové proměnné v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="78640-223">Display the value of the new variable, either by hovering over the new variable in the Script Pane, or by typing the new variable in the Console Pane.</span></span>

<span data-ttu-id="78640-224">Například zobrazit hodnotu $MyInvocation proměnné ve skriptu, hodnota přiřadit nové proměnné, jako je například $scriptname a poté najeďte myší na nebo zadejte proměnnou $scriptname zobrazíte jeho hodnotu.</span><span class="sxs-lookup"><span data-stu-id="78640-224">For example, to display the value of the $MyInvocation variable, in the script, assign the value to a new variable, such as $scriptname, and then hover over or type the $scriptname variable to display its value.</span></span>

```powershell
# In C:\ps-test\MyScript.ps1
$scriptname = $MyInvocation.MyCommand.Path
```

```output
# In the Console Pane:
PS> .\MyScript.ps1
PS> $scriptname
C:\ps-test\MyScript.ps1
```

## <a name="see-also"></a><span data-ttu-id="78640-225">Viz také</span><span class="sxs-lookup"><span data-stu-id="78640-225">See Also</span></span>

- [<span data-ttu-id="78640-226">Seznámení s prostředím Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="78640-226">Exploring the Windows PowerShell ISE</span></span>](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)