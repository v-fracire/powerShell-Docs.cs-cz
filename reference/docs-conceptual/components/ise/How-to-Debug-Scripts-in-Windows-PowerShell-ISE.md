---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Ladění skriptů v prostředí Windows PowerShell ISE
ms.openlocfilehash: b7af2de83a3f796a2057514e36ad8b74367e8ce2
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404082"
---
# <a name="how-to-debug-scripts-in-windows-powershell-ise"></a><span data-ttu-id="15d0e-103">Ladění skriptů v prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="15d0e-103">How to Debug Scripts in Windows PowerShell ISE</span></span>

<span data-ttu-id="15d0e-104">Tento článek popisuje, jak pomocí Windows Powershellu integrovaném skriptovacím prostředí (ISE) vizuální ladění funkcí ladění skriptů v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="15d0e-104">This article describes how to debug scripts on a local computer by using the Windows PowerShell Integrated Scripting Environment (ISE) visual debugging features.</span></span>

## <a name="how-to-manage-breakpoints"></a><span data-ttu-id="15d0e-105">Jak spravovat zarážky</span><span class="sxs-lookup"><span data-stu-id="15d0e-105">How to manage breakpoints</span></span>

<span data-ttu-id="15d0e-106">Zarážka je určené místo ve skriptu, ve kterém chcete operace pozastavit, takže můžete zkontrolovat aktuální stav proměnné a prostředí, ve kterém je spuštěn skript.</span><span class="sxs-lookup"><span data-stu-id="15d0e-106">A breakpoint is a designated spot in a script where you would like operation to pause so that you can examine the current state of the variables and the environment in which your script is running.</span></span> <span data-ttu-id="15d0e-107">Jakmile váš skript je pozastaveno zarážku, můžete spouštět příkazy v podokně konzoly pro zjištění stavu vašeho skriptu.</span><span class="sxs-lookup"><span data-stu-id="15d0e-107">Once your script is paused by a breakpoint, you can run commands in the Console Pane to examine the state of your script.</span></span>  <span data-ttu-id="15d0e-108">Můžete výstup proměnné nebo spustit další příkazy.</span><span class="sxs-lookup"><span data-stu-id="15d0e-108">You can output variables or run other commands.</span></span> <span data-ttu-id="15d0e-109">Dokonce můžete upravit hodnotu proměnné, které jsou viditelné pro kontext aktuálně spuštěného skriptu.</span><span class="sxs-lookup"><span data-stu-id="15d0e-109">You can even modify the value of any variables that are visible to the context of the currently running script.</span></span> <span data-ttu-id="15d0e-110">Po kontrole, co chcete zobrazit, můžete obnovit operace skriptu.</span><span class="sxs-lookup"><span data-stu-id="15d0e-110">After you have examined what you want to see, you can resume operation of the script.</span></span>

<span data-ttu-id="15d0e-111">Tři typy zarážky můžete nastavit v ladicím prostředí Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="15d0e-111">You can set three types of breakpoints in the Windows PowerShell debugging environment:</span></span>

1. <span data-ttu-id="15d0e-112">**Řádek zarážky**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-112">**Line breakpoint**.</span></span> <span data-ttu-id="15d0e-113">Skript pozastaví při dosažení řádku určené během operace skriptu</span><span class="sxs-lookup"><span data-stu-id="15d0e-113">The script pauses when the designated line is reached during the operation of the script</span></span>

2. <span data-ttu-id="15d0e-114">**Zarážka v proměnné.**</span><span class="sxs-lookup"><span data-stu-id="15d0e-114">**Variable breakpoint.**</span></span> <span data-ttu-id="15d0e-115">Skript pozastaví pokaždé, když se změní hodnota proměnné určené.</span><span class="sxs-lookup"><span data-stu-id="15d0e-115">The script pauses whenever the designated variable's value changes.</span></span>

3. <span data-ttu-id="15d0e-116">**Příkaz zarážku.**</span><span class="sxs-lookup"><span data-stu-id="15d0e-116">**Command breakpoint.**</span></span> <span data-ttu-id="15d0e-117">Skript pozastaví pokaždé, když určený příkaz bude spuštěn při operaci skriptu.</span><span class="sxs-lookup"><span data-stu-id="15d0e-117">The script pauses whenever the designated command is about to be run during the operation of the script.</span></span> <span data-ttu-id="15d0e-118">Může obsahovat parametry dál filtrovat zarážky pouze operace, které chcete.</span><span class="sxs-lookup"><span data-stu-id="15d0e-118">It can include parameters to further filter the breakpoint to only the operation you want.</span></span> <span data-ttu-id="15d0e-119">Příkaz může být také funkce, které jste vytvořili.</span><span class="sxs-lookup"><span data-stu-id="15d0e-119">The command can also be a function you created.</span></span>

<span data-ttu-id="15d0e-120">Z těchto v prostředí Windows PowerShell ISE ladění lze nastavit pouze řádek zarážky pomocí nabídky nebo pomocí klávesové zkratky.</span><span class="sxs-lookup"><span data-stu-id="15d0e-120">Of these, in the Windows PowerShell ISE debugging environment, only line breakpoints can be set by using the menu or the keyboard shortcuts.</span></span> <span data-ttu-id="15d0e-121">Další dva druhy zarážky můžete nastavit, ale jsou nastavené v podokně konzoly pomocí [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) rutiny.</span><span class="sxs-lookup"><span data-stu-id="15d0e-121">The other two types of breakpoints can be set, but they are set from the Console Pane by using the [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) cmdlet.</span></span> <span data-ttu-id="15d0e-122">Tato část popisuje, jak můžete provádět ladění úlohy v prostředí Windows PowerShell ISE pomocí nabídky, pokud je k dispozici a provádět širší škálu příkazy z podokna konzoly pomocí skriptování.</span><span class="sxs-lookup"><span data-stu-id="15d0e-122">This section describes how you can perform debugging tasks in Windows PowerShell ISE by using the menus where available, and perform a wider range of commands from the Console Pane by using scripting.</span></span>

### <a name="to-set-a-breakpoint"></a><span data-ttu-id="15d0e-123">Chcete-li nastavit zarážku</span><span class="sxs-lookup"><span data-stu-id="15d0e-123">To set a breakpoint</span></span>

<span data-ttu-id="15d0e-124">Zarážku lze nastavit ve skriptu, až po se uložil.</span><span class="sxs-lookup"><span data-stu-id="15d0e-124">A breakpoint can be set in a script only after it has been saved.</span></span> <span data-ttu-id="15d0e-125">Klikněte pravým tlačítkem na řádek, ve které chcete nastavit zarážku řádek a potom klikněte na **Přepnout zarážku**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-125">Right-click the line where you want to set a line breakpoint, and then click **Toggle Breakpoint**.</span></span> <span data-ttu-id="15d0e-126">Nebo klikněte na řádek, ve které chcete nastavit zarážku řádku a stisknutím klávesy **F9** nebo na **ladění** nabídky, klikněte na tlačítko **Přepnout zarážku**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-126">Or, click the line where you want to set a line breakpoint, and press **F9** or, on the **Debug** menu, click **Toggle Breakpoint**.</span></span>

<span data-ttu-id="15d0e-127">Následující skript je příklad, jak můžete nastavit zarážku proměnné z podokna konzoly pomocí [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) rutiny.</span><span class="sxs-lookup"><span data-stu-id="15d0e-127">The following script is an example of how you can set a variable breakpoint from the Console Pane by using the [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) cmdlet.</span></span>

```powershell
# This command sets a breakpoint on the Server variable in the Sample.ps1 script.
Set-PSBreakpoint -Script sample.ps1 -Variable Server
```

### <a name="list-all-breakpoints"></a><span data-ttu-id="15d0e-128">Vypsat všechny zarážky</span><span class="sxs-lookup"><span data-stu-id="15d0e-128">List all breakpoints</span></span>

<span data-ttu-id="15d0e-129">Zobrazí všechny zarážky v aktuální relaci Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="15d0e-129">Displays all breakpoints in the current Windows PowerShell session.</span></span>

<span data-ttu-id="15d0e-130">Na **ladění** nabídky, klikněte na tlačítko **seznamu zarážek**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-130">On the **Debug** menu, click **List Breakpoints**.</span></span> <span data-ttu-id="15d0e-131">Následující skript představuje příklad, o tom, jak můžete vytvořit seznam všechny zarážky v podokně konzoly pomocí [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) rutiny.</span><span class="sxs-lookup"><span data-stu-id="15d0e-131">The following script is an example of how you can list all breakpoints from the Console Pane by using the [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) cmdlet.</span></span>

```powershell
# This command lists all breakpoints in the current session.
Get-PSBreakpoint
```

### <a name="remove-a-breakpoint"></a><span data-ttu-id="15d0e-132">Odebrat zarážky</span><span class="sxs-lookup"><span data-stu-id="15d0e-132">Remove a breakpoint</span></span>

<span data-ttu-id="15d0e-133">Odebrání zarážku ji odstraní.</span><span class="sxs-lookup"><span data-stu-id="15d0e-133">Removing a breakpoint deletes it.</span></span>

<span data-ttu-id="15d0e-134">Pokud si myslíte, že budete chtít později znovu použít, zvažte [zakázat zarážku](#disable-a-breakpoint) jej místo toho.</span><span class="sxs-lookup"><span data-stu-id="15d0e-134">If you think you might want to use it again later, consider [Disable a Breakpoint](#disable-a-breakpoint) it instead.</span></span>
<span data-ttu-id="15d0e-135">Klikněte pravým tlačítkem na řádek, kde chcete odebrat zarážku a poté klikněte na tlačítko **Přepnout zarážku**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-135">Right-click the line where you want to remove a breakpoint, and then click **Toggle Breakpoint**.</span></span>
<span data-ttu-id="15d0e-136">Nebo klikněte na řádek, ve které chcete odebrat zarážku, a dále **ladění** nabídky, klikněte na tlačítko **Přepnout zarážku**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-136">Or, click the line where you want to remove a breakpoint, and on the **Debug** menu, click **Toggle Breakpoint**.</span></span>
<span data-ttu-id="15d0e-137">Následující skript představuje příklad, jak odebrat zarážku se zadaným ID z konzole pomocí [odebrat PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) rutiny.</span><span class="sxs-lookup"><span data-stu-id="15d0e-137">The following script is an example of how to remove a breakpoint with a specified ID from the Console Pane by using the [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet.</span></span>

```powershell
# This command deletes the breakpoint with breakpoint ID 2.
Remove-PSBreakpoint -Id 2
```

### <a name="remove-all-breakpoints"></a><span data-ttu-id="15d0e-138">Odebrat všechny zarážky</span><span class="sxs-lookup"><span data-stu-id="15d0e-138">Remove All Breakpoints</span></span>

<span data-ttu-id="15d0e-139">Chcete-li odebrat všechny zarážky, které jsou definované v aktuální relaci na **ladění** nabídky, klikněte na tlačítko **odebrat všechny zarážky**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-139">To remove all breakpoints defined in the current session, on the **Debug** menu, click **Remove All Breakpoints**.</span></span>

<span data-ttu-id="15d0e-140">Následující skript představuje příklad, jak odebrat všechny zarážky v podokně konzoly pomocí [odebrat PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) rutiny.</span><span class="sxs-lookup"><span data-stu-id="15d0e-140">The following script is an example of how to remove all breakpoints from the Console Pane by using the [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet.</span></span>

```powershell
# This command deletes all of the breakpoints in the current session.
Get-PSBreakpoint | Remove-PSBreakpoint
```

### <a name="disable-a-breakpoint"></a><span data-ttu-id="15d0e-141">Zakázat zarážku</span><span class="sxs-lookup"><span data-stu-id="15d0e-141">Disable a Breakpoint</span></span>

<span data-ttu-id="15d0e-142">Zakázat zarážku neodebere. ji vypne dokud není povoleno.</span><span class="sxs-lookup"><span data-stu-id="15d0e-142">Disabling a breakpoint does not remove it; it turns it off until it is enabled.</span></span>  <span data-ttu-id="15d0e-143">Zakázat zarážku konkrétního řádku, klikněte pravým tlačítkem na řádek, ve kterém chcete zakázat zarážku a poté klikněte na tlačítko **zakázat zarážku**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-143">To disable a specific line breakpoint, right-click the line where you want to disable a breakpoint, and then click **Disable Breakpoint**.</span></span> <span data-ttu-id="15d0e-144">Nebo klikněte na řádek, ve které chcete zakázat zarážku, a stiskněte klávesu **F9** nebo na **ladění** nabídky, klikněte na tlačítko **zakázat zarážku**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-144">Or, click the line where you want to disable a breakpoint, and press **F9** or, on the **Debug** menu, click **Disable Breakpoint**.</span></span> <span data-ttu-id="15d0e-145">Následující skript je příklad, jak odebrat zarážku se zadaným ID z podokna konzoly pomocí [zakázat PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) rutiny.</span><span class="sxs-lookup"><span data-stu-id="15d0e-145">The following script is an example of how you can remove a breakpoint with a specified ID from the Console Pane by using the [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet.</span></span>

```powershell
# This command disables the breakpoint with breakpoint ID 0.
Disable-PSBreakpoint -Id 0
```

### <a name="disable-all-breakpoints"></a><span data-ttu-id="15d0e-146">Zakázat všechny zarážky</span><span class="sxs-lookup"><span data-stu-id="15d0e-146">Disable All Breakpoints</span></span>

<span data-ttu-id="15d0e-147">Zakázat zarážku neodebere. ji vypne dokud není povoleno.</span><span class="sxs-lookup"><span data-stu-id="15d0e-147">Disabling a breakpoint does not remove it; it turns it off until it is enabled.</span></span>  <span data-ttu-id="15d0e-148">Chcete-li zakázat všechny zarážky v aktuální relaci, na **ladění** nabídky, klikněte na tlačítko **zakázat všechny zarážky**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-148">To disable all breakpoints in the current session, on the **Debug** menu, click **Disable all Breakpoints**.</span></span> <span data-ttu-id="15d0e-149">Následující skript představuje příklad, o tom, jak můžete zakázat všechny zarážky v podokně konzoly pomocí [zakázat PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) rutiny.</span><span class="sxs-lookup"><span data-stu-id="15d0e-149">The following script is an example of how you can disable all breakpoints from the Console Pane by using the [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet.</span></span>

```powershell
# This command disables all breakpoints in the current session.
# You can abbreviate this command as: "gbp | dbp".
Get-PSBreakpoint | Disable-PSBreakpoint
```

### <a name="enable-a-breakpoint"></a><span data-ttu-id="15d0e-150">Povolit zarážku</span><span class="sxs-lookup"><span data-stu-id="15d0e-150">Enable a Breakpoint</span></span>

<span data-ttu-id="15d0e-151">Pokud chcete povolit konkrétní zarážky, klikněte pravým tlačítkem na řádek, ve které chcete povolit zarážku a poté klikněte na tlačítko **povolit zarážku**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-151">To enable a specific breakpoint, right-click the line where you want to enable a breakpoint, and then click **Enable Breakpoint**.</span></span> <span data-ttu-id="15d0e-152">Nebo klikněte na řádek, ve které chcete povolit zarážku a potom stiskněte klávesu **F9** nebo na **ladění** nabídky, klikněte na tlačítko **povolit zarážku**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-152">Or, click the line where you want to enable a breakpoint, and then press **F9** or, on the **Debug** menu, click **Enable Breakpoint**.</span></span> <span data-ttu-id="15d0e-153">Následující skript představuje příklad, o tom, jak můžete povolit konkrétní zarážky v podokně konzoly pomocí [povolit PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) rutiny.</span><span class="sxs-lookup"><span data-stu-id="15d0e-153">The following script is an example of how you can enable specific breakpoints from the Console Pane by using the [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet.</span></span>

```powershell
# This command enables breakpoints with breakpoint IDs 0, 1, and 5.
Enable-PSBreakpoint -Id 0, 1, 5
```

### <a name="enable-all-breakpoints"></a><span data-ttu-id="15d0e-154">Povolit všechny zarážky</span><span class="sxs-lookup"><span data-stu-id="15d0e-154">Enable All Breakpoints</span></span>

<span data-ttu-id="15d0e-155">Povolit všechny zarážky, které jsou definované v aktuální relaci na **ladění** nabídky, klikněte na tlačítko **povolit všechny zarážky**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-155">To enable all breakpoints defined in the current session, on the **Debug** menu, click **Enable all Breakpoints**.</span></span> <span data-ttu-id="15d0e-156">Následující skript představuje příklad, o tom, jak můžete povolit všechny zarážky v podokně konzoly pomocí [povolit PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) rutiny.</span><span class="sxs-lookup"><span data-stu-id="15d0e-156">The following script is an example of how you can enable all breakpoints from the Console Pane by using the [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet.</span></span>

```powershell
# This command enables all breakpoints in the current session.
# You can abbreviate the command by using their aliases: "gbp | ebp".
Get-PSBreakpoint | Enable-PSBreakpoint
```

## <a name="how-to-manage-a-debugging-session"></a><span data-ttu-id="15d0e-157">Jak spravovat relace ladění</span><span class="sxs-lookup"><span data-stu-id="15d0e-157">How to manage a debugging session</span></span>

<span data-ttu-id="15d0e-158">Před zahájením ladění, je nutné nastavit jednu nebo více zarážek.</span><span class="sxs-lookup"><span data-stu-id="15d0e-158">Before you start debugging, you must set one or more breakpoints.</span></span> <span data-ttu-id="15d0e-159">Nelze nastavit zarážku, není-li uložit skript, který chcete ladit.</span><span class="sxs-lookup"><span data-stu-id="15d0e-159">You cannot set a breakpoint unless the script that you want to debug is saved.</span></span> <span data-ttu-id="15d0e-160">Pokyny na tom, jak nastavit zarážky, naleznete v tématu [Správa zarážky](#how-to-manage-breakpoints) nebo [Set-PSBreakpoint](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/set-psbreakpoint).</span><span class="sxs-lookup"><span data-stu-id="15d0e-160">For directions on of how to set a breakpoint, see [How to manage breakpoints](#how-to-manage-breakpoints) or [Set-PSBreakpoint](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/set-psbreakpoint).</span></span> <span data-ttu-id="15d0e-161">Po spuštění ladění, nelze upravit skript, dokud zastavíte ladění.</span><span class="sxs-lookup"><span data-stu-id="15d0e-161">After you start debugging, you cannot edit a script until you stop debugging.</span></span> <span data-ttu-id="15d0e-162">Skript, který má jednu nebo více zarážek nastavení se automaticky uloží před spuštěním.</span><span class="sxs-lookup"><span data-stu-id="15d0e-162">A script that has one or more breakpoints set is automatically saved before it is run.</span></span>

### <a name="to-start-debugging"></a><span data-ttu-id="15d0e-163">Pro spuštění ladění</span><span class="sxs-lookup"><span data-stu-id="15d0e-163">To start debugging</span></span>

<span data-ttu-id="15d0e-164">Stisknutím klávesy **F5** nebo na panelu nástrojů klikněte na tlačítko **spustit skript** ikonu, nebo na **ladění** klikněte na nabídku **Spustit/pokračovat**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-164">Press **F5** or, on the toolbar, click the **Run Script** icon, or on the **Debug** menu click **Run/Continue**.</span></span> <span data-ttu-id="15d0e-165">Skript se spustí, dokud nenarazí k první zarážce.</span><span class="sxs-lookup"><span data-stu-id="15d0e-165">The script runs until it encounters the first breakpoint.</span></span> <span data-ttu-id="15d0e-166">Operace v ní se pozastaví a zvýrazní řádek, na kterém je pozastavená.</span><span class="sxs-lookup"><span data-stu-id="15d0e-166">It pauses operation there and highlights the line on which it paused.</span></span>

### <a name="to-continue-debugging"></a><span data-ttu-id="15d0e-167">Pro pokračování v ladění</span><span class="sxs-lookup"><span data-stu-id="15d0e-167">To continue debugging</span></span>

<span data-ttu-id="15d0e-168">Stisknutím klávesy **F5** nebo na panelu nástrojů klikněte na tlačítko **spustit skript** ikonu, nebo na **ladění** nabídky, klikněte na tlačítko **Spustit/pokračovat** nebo na panelu konzoly zadejte **C** a potom stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-168">Press **F5** or, on the toolbar, click the **Run Script** icon, or on the **Debug** menu, click **Run/Continue** or, in the Console Pane, type **C** and then press **ENTER**.</span></span> <span data-ttu-id="15d0e-169">To způsobí, že skript bude moct být spuštěná na další zarážku nebo na konec skriptu, pokud nedojde k žádné další zarážky.</span><span class="sxs-lookup"><span data-stu-id="15d0e-169">This causes the script to continue running to the next breakpoint or to the end of the script if no further breakpoints are encountered.</span></span>

### <a name="to-view-the-call-stack"></a><span data-ttu-id="15d0e-170">Chcete-li zobrazit zásobník volání</span><span class="sxs-lookup"><span data-stu-id="15d0e-170">To view the call stack</span></span>

<span data-ttu-id="15d0e-171">Zásobník volání zobrazí aktuálního spuštění umístění ve skriptu.</span><span class="sxs-lookup"><span data-stu-id="15d0e-171">The call stack displays the current run location in the script.</span></span> <span data-ttu-id="15d0e-172">Pokud se ve funkci, která byla volána různých funkcí je spuštěný skript, pak, který je reprezentován v zobrazení dodatečné řádky ve výstupu.</span><span class="sxs-lookup"><span data-stu-id="15d0e-172">If the script is running in a function that was called by a different function, then that is represented in the display by additional rows in the output.</span></span> <span data-ttu-id="15d0e-173">Většina dolní řádek zobrazí původní skript a řádku v něm ve kterém byla volána funkce.</span><span class="sxs-lookup"><span data-stu-id="15d0e-173">The bottom-most row displays the original script and the line in it in which a function was called.</span></span> <span data-ttu-id="15d0e-174">Na další řádek nahoru ukazuje tuto funkci a řádek v něm ve kterém může mít jinou funkci zavolání.</span><span class="sxs-lookup"><span data-stu-id="15d0e-174">The next line up shows that function and the line in it in which another function might have been called.</span></span>  <span data-ttu-id="15d0e-175">Nejvrchnější řádek zobrazuje aktuální kontext aktuálního řádku, na kterém je nastavena zarážka.</span><span class="sxs-lookup"><span data-stu-id="15d0e-175">The top-most row shows the current context of the current line on which the breakpoint is set.</span></span>

<span data-ttu-id="15d0e-176">Během pozastavení, chcete-li zobrazit aktuální zásobník volání, stiskněte **CTRL + SHIFT + D** nebo na **ladění** nabídky, klikněte na tlačítko **zobrazit zásobník volání** nebo na panelu konzoly zadejte **tis.**  a potom stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-176">While paused, to see the current call stack, press **CTRL+SHIFT+D** or, on the **Debug** menu, click **Display Call Stack** or, in the Console Pane, type **K** and then press **ENTER**.</span></span>

### <a name="to-stop-debugging"></a><span data-ttu-id="15d0e-177">Chcete zastavit ladění</span><span class="sxs-lookup"><span data-stu-id="15d0e-177">To stop debugging</span></span>

<span data-ttu-id="15d0e-178">Stisknutím klávesy **SHIFT + F5** nebo na **ladění** nabídky, klikněte na tlačítko **zastavit ladicí program**, nebo na panelu konzoly zadejte **Q** a potom stiskněte klávesu  **Zadejte**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-178">Press **SHIFT-F5** or, on the **Debug** menu, click **Stop Debugger**, or, in the Console Pane, type **Q** and then press **ENTER**.</span></span>

## <a name="how-to-step-over-step-into-and-step-out-while-debugging"></a><span data-ttu-id="15d0e-179">Krokovat přes, Krokovat s vnořením a Krokovat s Vystoupením při ladění</span><span class="sxs-lookup"><span data-stu-id="15d0e-179">How to step over, step into, and step out while debugging</span></span>

<span data-ttu-id="15d0e-180">Krokování je proces spuštěný jeden příkaz v čase.</span><span class="sxs-lookup"><span data-stu-id="15d0e-180">Stepping is the process of running one statement at a time.</span></span> <span data-ttu-id="15d0e-181">Můžete zastavit na řádek kódu a zkoumat hodnoty proměnné a stav systému.</span><span class="sxs-lookup"><span data-stu-id="15d0e-181">You can stop on a line of code, and examine the values of variables and the state of the system.</span></span> <span data-ttu-id="15d0e-182">Následující tabulka popisuje běžné úlohy ladění jako je například krokování přes, krokování a krokování navýšení kapacity.</span><span class="sxs-lookup"><span data-stu-id="15d0e-182">The following table describes common debugging tasks such as stepping over, stepping into, and stepping out.</span></span>

| <span data-ttu-id="15d0e-183">Ladění úloh</span><span class="sxs-lookup"><span data-stu-id="15d0e-183">Debugging Task</span></span> | <span data-ttu-id="15d0e-184">Popis</span><span class="sxs-lookup"><span data-stu-id="15d0e-184">Description</span></span> | <span data-ttu-id="15d0e-185">Jak provést v prostředí PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="15d0e-185">How to accomplish it in PowerShell ISE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="15d0e-186">**Krokovat s vnořením**</span><span class="sxs-lookup"><span data-stu-id="15d0e-186">**Step Into**</span></span> | <span data-ttu-id="15d0e-187">Aktuální příkaz spustí a zastaví se na další příkaz.</span><span class="sxs-lookup"><span data-stu-id="15d0e-187">Executes the current statement and then stops at the next statement.</span></span> <span data-ttu-id="15d0e-188">Pokud je aktuální příkaz funkci nebo volání skriptu a ladicí program vstoupí do této funkce nebo skriptu, jinak se zastaví na další příkaz.</span><span class="sxs-lookup"><span data-stu-id="15d0e-188">If the current statement is a function or script call, then the debugger steps into that function or script, otherwise it stops at the next statement.</span></span> | <span data-ttu-id="15d0e-189">Stisknutím klávesy **F11** nebo na **ladění** nabídky, klikněte na tlačítko **Krokovat s vnořením**, nebo na panelu konzoly zadejte **S** a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-189">Press **F11** or, on the **Debug** menu, click **Step Into**, or in the Console Pane, type **S** and press **ENTER**.</span></span> |
| <span data-ttu-id="15d0e-190">**Krok přes**</span><span class="sxs-lookup"><span data-stu-id="15d0e-190">**Step Over**</span></span> | <span data-ttu-id="15d0e-191">Aktuální příkaz spustí a zastaví se na další příkaz.</span><span class="sxs-lookup"><span data-stu-id="15d0e-191">Executes the current statement and then stops at the next statement.</span></span> <span data-ttu-id="15d0e-192">Pokud je aktuální příkaz funkci nebo volání skriptu a ladicí program provede celou funkce nebo skriptu a zastaví na další příkaz následující po volání funkce.</span><span class="sxs-lookup"><span data-stu-id="15d0e-192">If the current statement is a function or script call, then the debugger executes the whole function or script, and it stops at the next statement after the function call.</span></span> | <span data-ttu-id="15d0e-193">Stisknutím klávesy **F10** nebo na **ladění** nabídky, klikněte na tlačítko **Krokovat s přeskočením**, nebo na panelu konzoly zadejte **V** a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-193">Press **F10** or, on the **Debug** menu, click **Step Over**, or in the Console Pane, type **V** and press **ENTER**.</span></span> |
| <span data-ttu-id="15d0e-194">**Krokovat s Vystoupením**</span><span class="sxs-lookup"><span data-stu-id="15d0e-194">**Step Out**</span></span> | <span data-ttu-id="15d0e-195">Kroky aktuální funkci a nahoru o jednu úroveň Pokud vnořené funkce.</span><span class="sxs-lookup"><span data-stu-id="15d0e-195">Steps out of the current function and up one level if the function is nested.</span></span> <span data-ttu-id="15d0e-196">Pokud se v hlavní části skript provádí na konci nebo až k další zarážce.</span><span class="sxs-lookup"><span data-stu-id="15d0e-196">If in the main body, the script is executed to the end, or to the next breakpoint.</span></span> <span data-ttu-id="15d0e-197">Přeskočené příkazy se provedl, ale ne prošli.</span><span class="sxs-lookup"><span data-stu-id="15d0e-197">The skipped statements are executed, but not stepped through.</span></span> | <span data-ttu-id="15d0e-198">Stisknutím klávesy **SHIFT + F11**, nebo **ladění** nabídky, klikněte na tlačítko **Krokovat s Vystoupením**, nebo na panelu konzoly zadejte **O** a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-198">Press **SHIFT+F11**, or on the **Debug** menu, click **Step Out**, or in the Console Pane, type **O** and press **ENTER**.</span></span> |
| <span data-ttu-id="15d0e-199">**Pokračovat**</span><span class="sxs-lookup"><span data-stu-id="15d0e-199">**Continue**</span></span> | <span data-ttu-id="15d0e-200">Pokračuje v provádění na konec nebo až k další zarážce.</span><span class="sxs-lookup"><span data-stu-id="15d0e-200">Continues execution to the end, or to the next breakpoint.</span></span> <span data-ttu-id="15d0e-201">Přeskočené funkce a volání jsou provedeny, ale ne prošli.</span><span class="sxs-lookup"><span data-stu-id="15d0e-201">The skipped functions and invocations are executed, but not stepped through.</span></span> | <span data-ttu-id="15d0e-202">Stisknutím klávesy **F5** nebo na **ladění** nabídky, klikněte na tlačítko **Spustit/pokračovat**, nebo na panelu konzoly zadejte **C** a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-202">Press **F5** or, on the **Debug** menu, click **Run/Continue**, or in the Console Pane, type **C** and press **ENTER**.</span></span> |

## <a name="how-to-display-the-values-of-variables-while-debugging"></a><span data-ttu-id="15d0e-203">Způsob zobrazení hodnot proměnných při ladění</span><span class="sxs-lookup"><span data-stu-id="15d0e-203">How to display the values of variables while debugging</span></span>

<span data-ttu-id="15d0e-204">Jak krokovat kód, můžete zobrazit aktuální hodnoty proměnných ve skriptu.</span><span class="sxs-lookup"><span data-stu-id="15d0e-204">You can display the current values of variables in the script as you step through the code.</span></span>

### <a name="to-display-the-values-of-standard-variables"></a><span data-ttu-id="15d0e-205">K zobrazení hodnot proměnných standard</span><span class="sxs-lookup"><span data-stu-id="15d0e-205">To display the values of standard variables</span></span>

<span data-ttu-id="15d0e-206">Použijte jednu z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="15d0e-206">Use one of the following methods:</span></span>

- <span data-ttu-id="15d0e-207">V podokně se skriptem najeďte myší proměnnou, a zobrazit jeho hodnotu jako popisku tlačítka.</span><span class="sxs-lookup"><span data-stu-id="15d0e-207">In the Script Pane, hover over the variable to display its value as a tool tip.</span></span>

- <span data-ttu-id="15d0e-208">V podokně konzoly, zadejte název proměnné a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="15d0e-208">In the Console Pane, type the variable name and press **ENTER**.</span></span>

<span data-ttu-id="15d0e-209">Všechna podokna v prostředí ISE jsou vždy ve stejném oboru.</span><span class="sxs-lookup"><span data-stu-id="15d0e-209">All panes in ISE are always in the same scope.</span></span> <span data-ttu-id="15d0e-210">Proto v při ladění skriptu, spouštět příkazy, které zadáte v podokně konzoly v oboru skriptu.</span><span class="sxs-lookup"><span data-stu-id="15d0e-210">Therefore, while you are debugging a script, the commands that you type in the Console Pane run in script scope.</span></span> <span data-ttu-id="15d0e-211">To umožňuje použití Pokokna konzoly můžete najít hodnoty proměnných a volání funkcí, které jsou definovány pouze ve skriptu.</span><span class="sxs-lookup"><span data-stu-id="15d0e-211">This allows you to use the Console Pane to find the values of variables and call functions that are defined only in the script.</span></span>

### <a name="to-display-the-values-of-automatic-variables"></a><span data-ttu-id="15d0e-212">Chcete-li zobrazit hodnoty automatických proměnných</span><span class="sxs-lookup"><span data-stu-id="15d0e-212">To display the values of automatic variables</span></span>

<span data-ttu-id="15d0e-213">Předchozí postup můžete použít k zobrazení hodnoty téměř všech proměnných při ladění skriptu.</span><span class="sxs-lookup"><span data-stu-id="15d0e-213">You can use the preceding method to display the value of almost all variables while you are debugging a script.</span></span> <span data-ttu-id="15d0e-214">Tyto metody nebude fungovat pro následující automatických proměnných.</span><span class="sxs-lookup"><span data-stu-id="15d0e-214">However, these methods do not work for the following automatic variables.</span></span>

- <span data-ttu-id="15d0e-215">$_</span><span class="sxs-lookup"><span data-stu-id="15d0e-215">$_</span></span>

- <span data-ttu-id="15d0e-216">$Input</span><span class="sxs-lookup"><span data-stu-id="15d0e-216">$Input</span></span>

- <span data-ttu-id="15d0e-217">$MyInvocation</span><span class="sxs-lookup"><span data-stu-id="15d0e-217">$MyInvocation</span></span>

- <span data-ttu-id="15d0e-218">$PSBoundParameters</span><span class="sxs-lookup"><span data-stu-id="15d0e-218">$PSBoundParameters</span></span>

- <span data-ttu-id="15d0e-219">$Args</span><span class="sxs-lookup"><span data-stu-id="15d0e-219">$Args</span></span>

<span data-ttu-id="15d0e-220">Pokud se pokusíte zobrazit hodnotu kterékoli z těchto proměnných, získejte hodnotu této proměnné pro interní kanálu ladicí program používá, nikoli hodnotu proměnné ve skriptu.</span><span class="sxs-lookup"><span data-stu-id="15d0e-220">If you try to display the value of any of these variables, you get the value of that variable for in an internal pipeline the debugger uses, not the value of the variable in the script.</span></span> <span data-ttu-id="15d0e-221">Můžete alternativně vyřešit to několika proměnných ($_, $Input, $MyInvocation, $PSBoundParameters a $Args) následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="15d0e-221">You can work around this for a few variables ($_, $Input, $MyInvocation, $PSBoundParameters, and $Args) by using the following method:</span></span>

1. <span data-ttu-id="15d0e-222">Ve skriptu přiřadíte hodnotu proměnné automatické nové proměnné.</span><span class="sxs-lookup"><span data-stu-id="15d0e-222">In the script, assign the value of the automatic variable to a new variable.</span></span>

2. <span data-ttu-id="15d0e-223">Zobrazte hodnotu nové proměnné ukazatele myši na novou proměnnou z podokna skriptu, nebo tak, že zadáte nové proměnné v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="15d0e-223">Display the value of the new variable, either by hovering over the new variable in the Script Pane, or by typing the new variable in the Console Pane.</span></span>

<span data-ttu-id="15d0e-224">Například k zobrazení hodnoty $MyInvocation proměnné ve skriptu, přiřaďte hodnotu nové proměnné, jako je například $scriptname a pak najeďte myší nebo zadejte proměnnou $scriptname k zobrazení jeho hodnoty.</span><span class="sxs-lookup"><span data-stu-id="15d0e-224">For example, to display the value of the $MyInvocation variable, in the script, assign the value to a new variable, such as $scriptname, and then hover over or type the $scriptname variable to display its value.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="15d0e-225">Viz také</span><span class="sxs-lookup"><span data-stu-id="15d0e-225">See Also</span></span>

- [<span data-ttu-id="15d0e-226">Seznámení s prostředím Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="15d0e-226">Exploring the Windows PowerShell ISE</span></span>](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)