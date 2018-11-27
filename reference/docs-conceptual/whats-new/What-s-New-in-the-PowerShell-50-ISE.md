---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Co je nového ve PowerShell 5.0 ISE
ms.assetid: 38648d47-7c27-4b37-a40e-ad29948519c2
ms.openlocfilehash: f05e3f3f95c8ceec6e843b8a1c79e6f092e1b87b
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320580"
---
# <a name="what39s-new-in-the-windows-powershell-ise"></a><span data-ttu-id="37ace-103">Co&#39;nového ve Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="37ace-103">What&#39;s New in the Windows PowerShell ISE</span></span>
<span data-ttu-id="37ace-104">Toto téma popisuje nové a aktualizované funkce, které byly zavedeny ve verzích systému Windows Powershellu integrovaném skriptovacím prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="37ace-104">This topic explains the new and updated features that have been introduced in versions of Windows PowerShell  Integrated Scripting Environment (ISE).</span></span>

## <a name="feature-description"></a><span data-ttu-id="37ace-105">Popis funkce</span><span class="sxs-lookup"><span data-stu-id="37ace-105">Feature description</span></span>
<span data-ttu-id="37ace-106">Windows PowerShell ISE je hostitelská aplikace, která umožňuje zapisovat, spouštět a testovat skripty a moduly v grafickém jednoduchá a intuitivní prostředí.</span><span class="sxs-lookup"><span data-stu-id="37ace-106">The Windows PowerShell ISE is a host application that enables you to write, run, and test scripts and modules in a graphical and intuitive environment.</span></span> <span data-ttu-id="37ace-107">Kartu klíčových funkcí, jako je například barevné zvýrazňování syntaxe, dokončování, vizuální ladění, dodržování předpisů kódování Unicode a kontextová nápověda poskytují celou řadu možností skriptování.</span><span class="sxs-lookup"><span data-stu-id="37ace-107">Key features such as syntax-coloring, tab completion, visual debugging, Unicode compliance, and context-sensitive Help provide a rich scripting experience.</span></span>

<span data-ttu-id="37ace-108">Přehled Windows PowerShell ISE, naleznete v tématu [přehled Windows Powershellu Integrované skriptovací prostředí](https://technet.microsoft.com/library/3c1892c2-bf84-4cb6-af26-1f453be9e671).</span><span class="sxs-lookup"><span data-stu-id="37ace-108">For an overview of Windows PowerShell ISE, see [Windows PowerShell Integrated Scripting Environment overview](https://technet.microsoft.com/library/3c1892c2-bf84-4cb6-af26-1f453be9e671).</span></span>

## <a name="new-and-changed-functionality-in-windows-powershell-ise"></a><span data-ttu-id="37ace-109">Nové a změněné funkce v prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="37ace-109">New and changed functionality in Windows PowerShell ISE</span></span>
<span data-ttu-id="37ace-110">Následující tabulka uvádí nové a změněné funkce pro tuto verzi Windows PowerShell ISE v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37ace-110">The following table lists the new and changed features for this release of Windows PowerShell ISE in Windows PowerShell.</span></span>

|<span data-ttu-id="37ace-111">Vlastnost/funkce</span><span class="sxs-lookup"><span data-stu-id="37ace-111">Feature/functionality</span></span>|<span data-ttu-id="37ace-112">Windows PowerShell ISE 4.0</span><span class="sxs-lookup"><span data-stu-id="37ace-112">Windows PowerShell ISE 4.0</span></span>|<span data-ttu-id="37ace-113">Windows PowerShell ISE 3.0</span><span class="sxs-lookup"><span data-stu-id="37ace-113">Windows PowerShell ISE 3.0</span></span>|<span data-ttu-id="37ace-114">ISE Windows Powershellu 2.0</span><span class="sxs-lookup"><span data-stu-id="37ace-114">Windows PowerShell ISE 2.0</span></span>|
|--------------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
|<span data-ttu-id="37ace-115">**[IntelliSense](#intellisense)**</span><span class="sxs-lookup"><span data-stu-id="37ace-115">**[IntelliSense](#intellisense)**</span></span>|<span data-ttu-id="37ace-116">X</span><span class="sxs-lookup"><span data-stu-id="37ace-116">X</span></span>|<span data-ttu-id="37ace-117">X</span><span class="sxs-lookup"><span data-stu-id="37ace-117">X</span></span>||
|<span data-ttu-id="37ace-118">**[Fragmenty kódu](#snippets)**</span><span class="sxs-lookup"><span data-stu-id="37ace-118">**[Snippets](#snippets)**</span></span>|<span data-ttu-id="37ace-119">X</span><span class="sxs-lookup"><span data-stu-id="37ace-119">X</span></span>|<span data-ttu-id="37ace-120">X</span><span class="sxs-lookup"><span data-stu-id="37ace-120">X</span></span>||
|<span data-ttu-id="37ace-121">**[Doplňkové nástroje](#add-on-tools)**</span><span class="sxs-lookup"><span data-stu-id="37ace-121">**[Add-on Tools](#add-on-tools)**</span></span>|<span data-ttu-id="37ace-122">X</span><span class="sxs-lookup"><span data-stu-id="37ace-122">X</span></span>|<span data-ttu-id="37ace-123">X</span><span class="sxs-lookup"><span data-stu-id="37ace-123">X</span></span>||
|<span data-ttu-id="37ace-124">**[Správce restartování a automatického ukládání](#restart-manager-and-auto-save)**</span><span class="sxs-lookup"><span data-stu-id="37ace-124">**[Restart Manager and Auto-save](#restart-manager-and-auto-save)**</span></span>|<span data-ttu-id="37ace-125">X</span><span class="sxs-lookup"><span data-stu-id="37ace-125">X</span></span>|<span data-ttu-id="37ace-126">X</span><span class="sxs-lookup"><span data-stu-id="37ace-126">X</span></span>||
|<span data-ttu-id="37ace-127">**[Seznam naposledy použitých](#most-recently-used-list)**</span><span class="sxs-lookup"><span data-stu-id="37ace-127">**[Most-recently used list](#most-recently-used-list)**</span></span>|<span data-ttu-id="37ace-128">X</span><span class="sxs-lookup"><span data-stu-id="37ace-128">X</span></span>|<span data-ttu-id="37ace-129">X</span><span class="sxs-lookup"><span data-stu-id="37ace-129">X</span></span>||
|<span data-ttu-id="37ace-130">**[Podokně konzoly](#console-pane)**</span><span class="sxs-lookup"><span data-stu-id="37ace-130">**[Console Pane](#console-pane)**</span></span>|<span data-ttu-id="37ace-131">X</span><span class="sxs-lookup"><span data-stu-id="37ace-131">X</span></span>|<span data-ttu-id="37ace-132">X</span><span class="sxs-lookup"><span data-stu-id="37ace-132">X</span></span>||
|<span data-ttu-id="37ace-133">**[Přepínače příkazového řádku](#command-line-switches)**</span><span class="sxs-lookup"><span data-stu-id="37ace-133">**[Command-line switches](#command-line-switches)**</span></span>|<span data-ttu-id="37ace-134">X</span><span class="sxs-lookup"><span data-stu-id="37ace-134">X</span></span>|<span data-ttu-id="37ace-135">X</span><span class="sxs-lookup"><span data-stu-id="37ace-135">X</span></span>||
|<span data-ttu-id="37ace-136">**[Nové funkce editoru](#new-editor-features)**</span><span class="sxs-lookup"><span data-stu-id="37ace-136">**[New editor features](#new-editor-features)**</span></span>|<span data-ttu-id="37ace-137">X</span><span class="sxs-lookup"><span data-stu-id="37ace-137">X</span></span>|<span data-ttu-id="37ace-138">X</span><span class="sxs-lookup"><span data-stu-id="37ace-138">X</span></span>||
|<span data-ttu-id="37ace-139">**[Nová okna programu Help viewer](#new-help-viewer-window)**</span><span class="sxs-lookup"><span data-stu-id="37ace-139">**[New Help viewer window](#new-help-viewer-window)**</span></span>|<span data-ttu-id="37ace-140">X</span><span class="sxs-lookup"><span data-stu-id="37ace-140">X</span></span>|<span data-ttu-id="37ace-141">X</span><span class="sxs-lookup"><span data-stu-id="37ace-141">X</span></span>||
|<span data-ttu-id="37ace-142">**[Rutiny show-– příkaz](#show-command-cmdlet)**</span><span class="sxs-lookup"><span data-stu-id="37ace-142">**[Show-Command cmdlet](#show-command-cmdlet)**</span></span>|<span data-ttu-id="37ace-143">X</span><span class="sxs-lookup"><span data-stu-id="37ace-143">X</span></span>|<span data-ttu-id="37ace-144">X</span><span class="sxs-lookup"><span data-stu-id="37ace-144">X</span></span>||

### <a name="intellisense"></a><span data-ttu-id="37ace-145">Technologie IntelliSense</span><span class="sxs-lookup"><span data-stu-id="37ace-145">IntelliSense</span></span>
<span data-ttu-id="37ace-146">**Přidáno v ISE 3.0**</span><span class="sxs-lookup"><span data-stu-id="37ace-146">**Added in ISE 3.0**</span></span>

<span data-ttu-id="37ace-147">Technologie IntelliSense je funkce automatického dokončování pomoc, který je součástí Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="37ace-147">IntelliSense is an automatic-completion assistance feature that is part of Windows PowerShell ISE.</span></span> <span data-ttu-id="37ace-148">Technologie IntelliSense zobrazí po kliknutí nabídky potenciálně odpovídajících rutin, parametry, hodnoty parametrů, soubory nebo složky při psaní.</span><span class="sxs-lookup"><span data-stu-id="37ace-148">IntelliSense displays clickable menus of potentially matching cmdlets, parameters, parameter values, files, or folders as you type.</span></span>

<span data-ttu-id="37ace-149">**Jakou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="37ace-149">**What value does this change add?**</span></span>

<span data-ttu-id="37ace-150">Přidání technologie IntelliSense je jednodušší zjistit rutiny a syntaxe, použijete-li vytvořit skripty Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="37ace-150">With the addition of IntelliSense, it is easier to discover cmdlets and syntax when you use Windows PowerShell ISE to create scripts.</span></span> <span data-ttu-id="37ace-151">Můžete také použít Windows PowerShell ISE další prostředí Windows PowerShell při vytváření nové skripty.</span><span class="sxs-lookup"><span data-stu-id="37ace-151">You can also use Windows PowerShell ISE to learn Windows PowerShell while you create new scripts.</span></span>

<span data-ttu-id="37ace-152">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="37ace-152">**What works differently?**</span></span>

<span data-ttu-id="37ace-153">Po zadání rutiny Windows PowerShell ISE 3.0 nebo novější posuvný a kliknout, čímž nabídce se zobrazí, umožňuje procházet a vyberte příslušné příkazy.</span><span class="sxs-lookup"><span data-stu-id="37ace-153">When you type cmdlets in the Windows PowerShell ISE 3.0 or later, a scrollable and clickable menu displays, allowing you to browse and select the appropriate commands.</span></span>

### <a name="snippets"></a><span data-ttu-id="37ace-154">Fragmenty kódu</span><span class="sxs-lookup"><span data-stu-id="37ace-154">Snippets</span></span>
<span data-ttu-id="37ace-155">**Přidáno v ISE 3.0**</span><span class="sxs-lookup"><span data-stu-id="37ace-155">**Added in ISE 3.0**</span></span>

<span data-ttu-id="37ace-156">*Fragmenty kódu* jsou krátké části kód prostředí Windows PowerShell, který můžete vložit do skriptů v prostředí Windows PowerShell ISE vytvoříte.</span><span class="sxs-lookup"><span data-stu-id="37ace-156">*Snippets* are short sections of Windows PowerShell code that you can insert into the scripts you create in Windows PowerShell ISE.</span></span> <span data-ttu-id="37ace-157">Windows PowerShell ISE přednastavena výchozí fragmentů kódu.</span><span class="sxs-lookup"><span data-stu-id="37ace-157">Windows PowerShell ISE comes with a default set of snippets.</span></span> <span data-ttu-id="37ace-158">Fragmenty kódu můžete přidat pomocí **New-fragment** rutiny při práci v prostředí Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="37ace-158">You can add snippets by using the **New-Snippet** cmdlet while working in Windows PowerShell ISE.</span></span>

<span data-ttu-id="37ace-159">**Jakou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="37ace-159">**What value does this change add?**</span></span>

<span data-ttu-id="37ace-160">Pomocí fragmentů kódu můžete rychle sestavit a vytvářet skripty pro automatizaci prostředí.</span><span class="sxs-lookup"><span data-stu-id="37ace-160">By using snippets, you can quickly assemble and create scripts to automate your environment.</span></span>

<span data-ttu-id="37ace-161">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="37ace-161">**What works differently?**</span></span>

<span data-ttu-id="37ace-162">Na použití fragmenty kódu v prostředí Windows PowerShell 3.0 nebo novější, **upravit** nabídky, klikněte na tlačítko **spustit fragmenty**, nebo stiskněte klávesu **Ctrl-J**.</span><span class="sxs-lookup"><span data-stu-id="37ace-162">To use snippets in Windows PowerShell 3.0 or later, on the **Edit** menu, click **Start Snippets**, or press **Ctrl-J**.</span></span>

### <a name="add-on-tools"></a><span data-ttu-id="37ace-163">Doplňkové nástroje</span><span class="sxs-lookup"><span data-stu-id="37ace-163">Add-on tools</span></span>
<span data-ttu-id="37ace-164">**Přidáno v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="37ace-164">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="37ace-165">Windows PowerShell ISE teď podporuje doplněk nástroje, které jsou ovládacích prvků Windows Presentation Foundation (WPF), které jsou přidány pomocí objektového modelu.</span><span class="sxs-lookup"><span data-stu-id="37ace-165">Windows PowerShell ISE now supports add-on tools, which are Windows Presentation Foundation (WPF) controls that are added by using the object model.</span></span> <span data-ttu-id="37ace-166">Doplňkové nástroje lze zobrazit jako svislý nebo vodorovný podokno v konzole.</span><span class="sxs-lookup"><span data-stu-id="37ace-166">Add-on tools can be displayed as a vertical or horizontal pane in the console.</span></span> <span data-ttu-id="37ace-167">Více nástrojů pro doplněk v podokně se zobrazují jako ovládací prvek s kartami.</span><span class="sxs-lookup"><span data-stu-id="37ace-167">Multiple add-on tools in a pane are displayed as a tabbed control.</span></span> <span data-ttu-id="37ace-168">Můžete také přidat nebo odebrat doplňkové nástroje, které jsou vytvářeny stranami mimo společnost Microsoft.</span><span class="sxs-lookup"><span data-stu-id="37ace-168">You can also add or remove add-on tools that are produced by non-Microsoft parties.</span></span> <span data-ttu-id="37ace-169">Další informace o tom, jak importovat nebo odebrání nástrojů pro doplněk, naleznete v tématu [operacích Windows Powershellu ISE](https://technet.microsoft.com/library/cc732148.aspx).</span><span class="sxs-lookup"><span data-stu-id="37ace-169">For more information about how to import or remove add-on tools, see [Windows PowerShell ISE Operations](https://technet.microsoft.com/library/cc732148.aspx).</span></span>

<span data-ttu-id="37ace-170">**Jakou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="37ace-170">**What value does this change add?**</span></span>

<span data-ttu-id="37ace-171">Doplňky umožňují rozšířit a přizpůsobit pomocí nástrojů, které můžete vylepšení prostředí pro skriptování, nebo přidat funkci Windows PowerShell ISE Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="37ace-171">Add-ons allow you to extend and customize Windows PowerShell ISE with tools that can enhance your scripting experience or add functionality to Windows PowerShell ISE.</span></span>

<span data-ttu-id="37ace-172">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="37ace-172">**What works differently?**</span></span>

<span data-ttu-id="37ace-173">Prostředí Windows PowerShell ISE 3.0 a novější se dodávají s **příkazy** doplněk.</span><span class="sxs-lookup"><span data-stu-id="37ace-173">Windows PowerShell ISE 3.0 and later come with the **Commands** add-on.</span></span> <span data-ttu-id="37ace-174">**Příkazy** doplněk vám umožní procházet rutiny a nápovědu o rutiny – souběžně s **skript** a **konzoly** podoken.</span><span class="sxs-lookup"><span data-stu-id="37ace-174">The **Commands** add-on allows you to browse cmdlets, and access help about the cmdlets side-by-side with the **Script** and **Console** Panes.</span></span>

<span data-ttu-id="37ace-175">Další doplňky můžete najít pomocí **otevřít webovou stránku nástroje pro doplněk** příkaz **doplňky** nabídky.</span><span class="sxs-lookup"><span data-stu-id="37ace-175">Additional add-ons can be found by using the **Open Add-on Tools Website** command on the **Add-ons** menu.</span></span>

### <a name="restart-manager-and-auto-save"></a><span data-ttu-id="37ace-176">Restartovat správce a automatického ukládání</span><span class="sxs-lookup"><span data-stu-id="37ace-176">Restart manager and auto-save</span></span>
<span data-ttu-id="37ace-177">**Přidáno v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="37ace-177">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="37ace-178">Windows PowerShell ISE nyní automaticky ukládá otevřít skripty každé dvě minuty v samostatném umístění.</span><span class="sxs-lookup"><span data-stu-id="37ace-178">Windows PowerShell ISE now automatically saves your open scripts every two minutes, in a separate location.</span></span>  <span data-ttu-id="37ace-179">Pokud Windows PowerShell ISE přestane fungovat, nebo pokud operační systém se restartuje, po restartování prostředí Windows PowerShell ISE, obnoví otevřít skripty, které byly během poslední relace, i v případě, že skripty nebyly uloženy.</span><span class="sxs-lookup"><span data-stu-id="37ace-179">If Windows PowerShell ISE stops working, or if the operating system is restarted, after Windows PowerShell ISE restarts, it recovers scripts that were open in the last session, even if the scripts were not saved.</span></span>

<span data-ttu-id="37ace-180">Pokud chcete změnit interval automatické ukládání, spusťte následující příkaz na panelu konzoly: **$psise. Options.AutoSaveMinuteInterval**.</span><span class="sxs-lookup"><span data-stu-id="37ace-180">To change the automatic saving interval, run the following command in the Console pane: **$psise.Options.AutoSaveMinuteInterval**.</span></span>

<span data-ttu-id="37ace-181">**Jakou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="37ace-181">**What value does this change add?**</span></span>

<span data-ttu-id="37ace-182">Teď můžete pracovat v rámci Windows PowerShell ISE vědomím, že jsou otevřené skripty automaticky uložené v případě neočekávaného restartování.</span><span class="sxs-lookup"><span data-stu-id="37ace-182">You can now work within Windows PowerShell ISE knowing that your open scripts are automatically saved in the event of an unexpected restart.</span></span>

<span data-ttu-id="37ace-183">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="37ace-183">**What works differently?**</span></span>

<span data-ttu-id="37ace-184">Windows PowerShell ISE 2.0 nelze uložit skripty automaticky v případě restartování.</span><span class="sxs-lookup"><span data-stu-id="37ace-184">Windows PowerShell ISE 2.0 does not save the scripts automatically in the event of a restart.</span></span>

### <a name="most-recently-used-list"></a><span data-ttu-id="37ace-185">Seznam naposledy použitých</span><span class="sxs-lookup"><span data-stu-id="37ace-185">Most-recently used list</span></span>
<span data-ttu-id="37ace-186">**Přidáno v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="37ace-186">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="37ace-187">Windows PowerShell ISE teď má seznam naposledy použitých souborů.</span><span class="sxs-lookup"><span data-stu-id="37ace-187">Windows PowerShell ISE now has a most-recently used list for files.</span></span> <span data-ttu-id="37ace-188">Při otevření souboru v prostředí Windows PowerShell ISE, soubor je přidán do seznamu naposledy použitých na **souboru** nabídky.</span><span class="sxs-lookup"><span data-stu-id="37ace-188">When you open a file in Windows PowerShell ISE, the file is added to the most-recently used list on the **File** menu.</span></span>

<span data-ttu-id="37ace-189">Chcete-li změnit výchozí počet souborů v seznamu naposledy použitých, spusťte následující příkaz na panelu konzoly: **$psise. Options.MruCount**.</span><span class="sxs-lookup"><span data-stu-id="37ace-189">To change the default number of files in the most-recently used list, run the following command in the Console Pane: **$psise.Options.MruCount**.</span></span>

<span data-ttu-id="37ace-190">**Jakou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="37ace-190">**What value does this change add?**</span></span>

<span data-ttu-id="37ace-191">Seznam naposledy použitých teď můžete snadno přístup k souborům se často používá.</span><span class="sxs-lookup"><span data-stu-id="37ace-191">You can now use the most-recently used list to easily access your frequently-used files.</span></span>

<span data-ttu-id="37ace-192">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="37ace-192">**What works differently?**</span></span>

<span data-ttu-id="37ace-193">Windows PowerShell ISE 2.0 nemá seznam naposledy použitých.</span><span class="sxs-lookup"><span data-stu-id="37ace-193">Windows PowerShell ISE 2.0 does not have a most-recently used list.</span></span>

### <a name="console-pane"></a><span data-ttu-id="37ace-194">Podokně konzoly</span><span class="sxs-lookup"><span data-stu-id="37ace-194">Console Pane</span></span>
<span data-ttu-id="37ace-195">**Přidáno v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="37ace-195">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="37ace-196">Samostatný příkaz a výstupní podokna, které byly k dispozici v první verzi Windows PowerShell ISE byly zkombinovány do jediného konzoly.</span><span class="sxs-lookup"><span data-stu-id="37ace-196">The separate Command and Output Panes that were available in the first release of Windows PowerShell ISE have been combined into a single Console Pane.</span></span> <span data-ttu-id="37ace-197">V podokně konzoly je podobné jako u funkce a vzhled typické konzoly Windows Powershellu, ale zahrnuje následující vylepšení (většina jsou popsány v tomto tématu).</span><span class="sxs-lookup"><span data-stu-id="37ace-197">The Console Pane is similar in function and appearance to a typical Windows PowerShell console, but it includes the following enhancements (most are described in this topic).</span></span>

- <span data-ttu-id="37ace-198">Barevné zvýrazňování syntaxe pro vstupního textu (ne výstupní text), včetně syntaxe jazyka XML</span><span class="sxs-lookup"><span data-stu-id="37ace-198">Syntax coloring for input text (not output text), including XML syntax</span></span>

- <span data-ttu-id="37ace-199">Technologie IntelliSense</span><span class="sxs-lookup"><span data-stu-id="37ace-199">IntelliSense</span></span>

- <span data-ttu-id="37ace-200">Párování závorek</span><span class="sxs-lookup"><span data-stu-id="37ace-200">Brace matching</span></span>

- <span data-ttu-id="37ace-201">Označení chyb</span><span class="sxs-lookup"><span data-stu-id="37ace-201">Error indication</span></span>

- <span data-ttu-id="37ace-202">Plná podpora kódování Unicode</span><span class="sxs-lookup"><span data-stu-id="37ace-202">Full Unicode support</span></span>

- <span data-ttu-id="37ace-203">**F1** kontextové nápovědy</span><span class="sxs-lookup"><span data-stu-id="37ace-203">**F1** context-sensitive help</span></span>

- <span data-ttu-id="37ace-204">**CTRL + F1** kontextové Show-– příkaz</span><span class="sxs-lookup"><span data-stu-id="37ace-204">**Ctrl+F1** context-sensitive Show-Command</span></span>

- <span data-ttu-id="37ace-205">Složitým a podporu zprava doleva</span><span class="sxs-lookup"><span data-stu-id="37ace-205">Complex script and right-to-left support</span></span>

- <span data-ttu-id="37ace-206">Podpora písma</span><span class="sxs-lookup"><span data-stu-id="37ace-206">Font support</span></span>

- <span data-ttu-id="37ace-207">Přiblížení</span><span class="sxs-lookup"><span data-stu-id="37ace-207">Zoom</span></span>

- <span data-ttu-id="37ace-208">Režimy výběru řádku a výběru bloku</span><span class="sxs-lookup"><span data-stu-id="37ace-208">Line-select and block-select modes</span></span>

- <span data-ttu-id="37ace-209">Zachování zadaný obsah na příkazovém řádku po stisknutí klávesy **nahoru** šipku a zobrazte historii v konzole</span><span class="sxs-lookup"><span data-stu-id="37ace-209">Preservation of typed content at the command line when you press the **Up** arrow to view history in the console</span></span>

<span data-ttu-id="37ace-210">**Jakou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="37ace-210">**What value does this change add?**</span></span>

<span data-ttu-id="37ace-211">Přidání těchto změn podokně konzoly poskytuje prostředí skriptování, který je konzistentní s rozhraní konzoly.</span><span class="sxs-lookup"><span data-stu-id="37ace-211">The addition of these Console Pane changes provides a scripting experience that is more consistent with the console interface.</span></span>

<span data-ttu-id="37ace-212">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="37ace-212">**What works differently?**</span></span>

<span data-ttu-id="37ace-213">Windows PowerShell ISE 2.0 má samostatný příkaz a výstupní podokna.</span><span class="sxs-lookup"><span data-stu-id="37ace-213">Windows PowerShell ISE 2.0 has separate Command and Output Panes.</span></span>

### <a name="command-line-switches"></a><span data-ttu-id="37ace-214">Přepínače příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="37ace-214">Command-line switches</span></span>
<span data-ttu-id="37ace-215">**Přidáno v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="37ace-215">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="37ace-216">Pokud spustíte z příkazového řádku Windows PowerShell ISE (zadáním **powershell_ise.exe**), můžete přidat následující nové přepínače příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="37ace-216">If you start Windows PowerShell ISE from the command line (by typing **powershell_ise.exe**), you can add the following new command-line switches.</span></span>

- <span data-ttu-id="37ace-217">*-NoProfile*: spuštění Windows PowerShell ISE bez spuštění **$profile**</span><span class="sxs-lookup"><span data-stu-id="37ace-217">*-NoProfile*: Starts Windows PowerShell ISE without running **$profile**</span></span>

- <span data-ttu-id="37ace-218">*-Help*: Zobrazí okno nápovědy</span><span class="sxs-lookup"><span data-stu-id="37ace-218">*-Help*: Displays a Help window</span></span>

- <span data-ttu-id="37ace-219">*-mta*: spuštění Windows PowerShell ISE v režimu apartmentu s více vlákny.</span><span class="sxs-lookup"><span data-stu-id="37ace-219">*-mta*: Starts Windows PowerShell ISE in multithreaded apartment mode.</span></span> <span data-ttu-id="37ace-220">Výchozí režim operace pro Windows PowerShell ISE je jednovláknový apartment režimu nebo *- sta*.</span><span class="sxs-lookup"><span data-stu-id="37ace-220">The default operation mode for Windows PowerShell ISE is single-threaded apartment mode, or *-sta*.</span></span>

<span data-ttu-id="37ace-221">**Jakou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="37ace-221">**What value does this change add?**</span></span>

<span data-ttu-id="37ace-222">Přidání přepínačů příkazového řádku umožňuje řízení prostředí, ve kterém běží Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="37ace-222">The addition of these command-line switches allows you to control the environment in which the Windows PowerShell ISE runs.</span></span>

<span data-ttu-id="37ace-223">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="37ace-223">**What works differently?**</span></span>

<span data-ttu-id="37ace-224">Windows PowerShell ISE 2.0 nedokáže rozpoznat tyto přepínače příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="37ace-224">Windows PowerShell ISE 2.0 does not recognize these command-line switches.</span></span>

### <a name="new-editor-features"></a><span data-ttu-id="37ace-225">Nové funkce editoru</span><span class="sxs-lookup"><span data-stu-id="37ace-225">New editor features</span></span>
<span data-ttu-id="37ace-226">**Přidáno v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="37ace-226">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="37ace-227">Další úpravy funkce Windows PowerShell ISE zahrnují:</span><span class="sxs-lookup"><span data-stu-id="37ace-227">Other Windows PowerShell ISE editing features include:</span></span>

- <span data-ttu-id="37ace-228">**Barevné zvýrazňování syntaxe XML**Windows PowerShell ISE teď barvy syntaxe jazyka XML stejným způsobem, jak barvy syntaxe prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37ace-228">**XML syntax coloring**Windows PowerShell ISE now colors XML syntax in the same way as it colors Windows PowerShell syntax.</span></span>

- <span data-ttu-id="37ace-229">**Párování závorek** Windows PowerShell ISE zahrnuje párování složených závorek a zvýrazňování a je možné následujícím způsobem: (například pomocí **přejít na shodu** příkazu nebo **Ctrl +]** vyhledá pravé složené závorky, pokud máte vybrané levá složená závorka).</span><span class="sxs-lookup"><span data-stu-id="37ace-229">**Brace matching** Windows PowerShell ISE includes brace matching and highlighting, and can be used in the following ways: (for example, using the **Go to Match** command or **Ctrl + ]** locates the closing brace, if you have an opening brace selected).</span></span>

- <span data-ttu-id="37ace-230">**Zobrazení osnovy** podokně se skriptem podporuje sbalování, který umožňuje sbalení nebo kliknutím na tlačítko plus nebo mínus rozbalení části kódu přihlásí na levém okraji.</span><span class="sxs-lookup"><span data-stu-id="37ace-230">**Outline view** The Script Pane supports outlining, which allows collapsing or expanding sections of code by clicking plus or minus signs in the left margin.</span></span> <span data-ttu-id="37ace-231">Můžete použít složené závorky nebo **#region** a **#endregion** značky k označení začátku nebo konci do sbalitelného oddílu.</span><span class="sxs-lookup"><span data-stu-id="37ace-231">You can use braces or the **#region** and **#endregion** tags to mark the beginning or end of a collapsible section.</span></span> <span data-ttu-id="37ace-232">Chcete-li rozbalit nebo sbalit všechny oblasti, stiskněte **Ctrl + M**.</span><span class="sxs-lookup"><span data-stu-id="37ace-232">To expand or collapse all regions, press **Ctrl + M**.</span></span>

- <span data-ttu-id="37ace-233">**Přetáhnout myší úpravy textu**ISE Windows PowerShell teď podporuje přetažení úpravy textu.</span><span class="sxs-lookup"><span data-stu-id="37ace-233">**Drag and drop text editing**Windows PowerShell ISE now supports drag and drop text editing.</span></span> <span data-ttu-id="37ace-234">Můžete vybrat libovolný blok textu a přetáhněte tento text do jiného umístění v editoru nebo konzoly pro přesunutí text.</span><span class="sxs-lookup"><span data-stu-id="37ace-234">You can select any block of text and drag that text to another location in the editor or the console to move the text.</span></span> <span data-ttu-id="37ace-235">Pokud podržíte stisknutou klávesu Ctrl při přetahování vybraný text při uvolnění tlačítka myši text je zkopírován do nového umístění.</span><span class="sxs-lookup"><span data-stu-id="37ace-235">If you hold down the Ctrl key while you drag the selected text, when you release the mouse button the text is copied to the new location.</span></span> <span data-ttu-id="37ace-236">V této verzi systému Windows PowerShell ISE, stejně jako v předchozí verzi Windows PowerShell ISE Když přetahujete soubory na Windows PowerShell ISE Windows PowerShell ISE otevře soubor.</span><span class="sxs-lookup"><span data-stu-id="37ace-236">In this version of Windows PowerShell ISE, as well as the previous version of Windows PowerShell ISE, when you drag and drop files onto Windows PowerShell ISE, Windows PowerShell ISE opens the file.</span></span>

- <span data-ttu-id="37ace-237">**Analýza chybových** chybami Parsování jsou označeny červenou vlnovkou.</span><span class="sxs-lookup"><span data-stu-id="37ace-237">**Parse error display** Parse errors are indicated with red underlines.</span></span> <span data-ttu-id="37ace-238">Když najedete myší uvedené chyby, zobrazí text popisku problém, který byl nalezen v kódu.</span><span class="sxs-lookup"><span data-stu-id="37ace-238">When you hover over an indicated error, tooltip text displays the problem that was found in the code.</span></span>

- <span data-ttu-id="37ace-239">**Přiblížení** procento zvětšení konzoly "™ s obsahem lze nastavit pomocí posuvníku lupy (v pravém dolním rohu okno integrovaného skriptovacího prostředí Windows PowerShell) nebo zadáním příkazu **$psise.options.Zoom** v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="37ace-239">**Zoom** The zoom percentage of the console'™s content can be set by using the zoom slider (in the lower right corner of Windows PowerShell ISE window), or by entering the command **$psise.options.Zoom** in the Console Pane.</span></span>

- <span data-ttu-id="37ace-240">**Formátovaný text zkopírovat a vložit** kopírování do schránky ve Windows PowerShell ISE zachová písmo, velikost a informace o barvě původní výběru.</span><span class="sxs-lookup"><span data-stu-id="37ace-240">**Rich text copy and paste** Copying to the clipboard in Windows PowerShell ISE preserves the font, size, and color information of the original selection.</span></span>

- <span data-ttu-id="37ace-241">**Běr bloku** můžete vybrat blok textu, podržte stisknutou klávesu ALT a výběr textu v podokně skriptu pomocí myši nebo stisknutím klávesy **Alt + Shift + šipka**.</span><span class="sxs-lookup"><span data-stu-id="37ace-241">**Block selection** You can select a block of text by holding down the ALT key while selecting text in the Script Pane with your mouse, or by pressing **Alt+Shift+Arrow**.</span></span>

<span data-ttu-id="37ace-242">**Jakou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="37ace-242">**What value does this change add?**</span></span>

<span data-ttu-id="37ace-243">Další funkce úprav poskytovat konzistentní a výkonné prostředí pro úpravy.</span><span class="sxs-lookup"><span data-stu-id="37ace-243">The additional editing features provide a more consistent and powerful editing environment.</span></span>

<span data-ttu-id="37ace-244">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="37ace-244">**What works differently?**</span></span>

<span data-ttu-id="37ace-245">Tyto úpravy vylepšení nebyly přítomny v rozhraní Windows PowerShell ISE 2.0.</span><span class="sxs-lookup"><span data-stu-id="37ace-245">These editing enhancements were not present in Windows PowerShell ISE 2.0.</span></span>

### <a name="new-help-viewer-window"></a><span data-ttu-id="37ace-246">Nová okna programu Help viewer</span><span class="sxs-lookup"><span data-stu-id="37ace-246">New Help viewer window</span></span>
<span data-ttu-id="37ace-247">**Přidáno v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="37ace-247">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="37ace-248">Pokud stisknete **F1** při kurzor je v rutině, nebo máte součástí rutiny zvýrazněný, nového programu Help viewer, otevře se kontextové nápovědy o rutině zvýrazněné.</span><span class="sxs-lookup"><span data-stu-id="37ace-248">If you press **F1** when your cursor is in a cmdlet, or you have part of a cmdlet highlighted, the new Help viewer opens context-sensitive Help about the highlighted cmdlet.</span></span> <span data-ttu-id="37ace-249">Chcete-li zobrazit nápovědu Windows Powershellu o, zadejte **operátory** v podokně konzoly a poté stiskněte klávesu **F1**.</span><span class="sxs-lookup"><span data-stu-id="37ace-249">To display Windows PowerShell About help, type  **operators** in the console pane, and then press **F1**.</span></span>

<span data-ttu-id="37ace-250">Před použitím této funkce, stáhněte si nejnovější verze témata nápovědy pro Windows PowerShell na webu společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="37ace-250">Before you use this feature, download the most current version of Windows PowerShell Help topics from the Microsoft website.</span></span> <span data-ttu-id="37ace-251">Nejjednodušší způsob stahování témata nápovědy je spustit **Update-Help** rutiny v podokně konzoly při spuštění Windows PowerShell ISE jako správce.</span><span class="sxs-lookup"><span data-stu-id="37ace-251">The simplest method for downloading the Help topics is to run the **Update-Help** cmdlet in the Console Pane when running Windows PowerShell ISE as administrator.</span></span>

<span data-ttu-id="37ace-252">Kde je možné změnit **F1** klíče hledá nápovědy.</span><span class="sxs-lookup"><span data-stu-id="37ace-252">You can alter where the **F1** key looks for Help.</span></span> <span data-ttu-id="37ace-253">V **nástroje**/**možnosti** nabídky na **obecné nastavení** ve skupině **další nastavení**, můžete nastavit nebo zrušte zaškrtávací políčko **nahrazujícím obsah místní nápovědy online obsah**.</span><span class="sxs-lookup"><span data-stu-id="37ace-253">In the **Tools**/**Options** menu, on the **General Settings** tab, under **Other Settings**, you can set or clear the checkbox **Use local help content instead of online content**.</span></span> <span data-ttu-id="37ace-254">Pokud je zaškrtnuto, klient vyhledá pro rutinu Nápověda v nápovědě stažené nacházejí ve složce modulů.</span><span class="sxs-lookup"><span data-stu-id="37ace-254">If checked, then the client looks for the cmdlet Help in the downloaded Help found in the modules folder.</span></span>  <span data-ttu-id="37ace-255">Pokud políčko není zaškrtnuto, klient vyhledá v knihovně TechNet pro nápovědy k rutinám.</span><span class="sxs-lookup"><span data-stu-id="37ace-255">If the checkbox is cleared, then the client looks on the TechNet library for the cmdlet help.</span></span>

<span data-ttu-id="37ace-256">**Jakou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="37ace-256">**What value does this change add?**</span></span>

<span data-ttu-id="37ace-257">Kontextová nápověda, aniž byste museli opustit aktuální rutiny nebo skriptu poskytuje bezproblémové učení.</span><span class="sxs-lookup"><span data-stu-id="37ace-257">Context-sensitive Help without leaving your current cmdlet or script provides a seamless learning experience.</span></span>

<span data-ttu-id="37ace-258">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="37ace-258">**What works differently?**</span></span>

<span data-ttu-id="37ace-259">Stisknutím klávesy F1 v předchozích verzích Windows PowerShell ISE otevřít soubor nápovědy v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="37ace-259">Pressing F1 in previous versions of Windows PowerShell ISE opened the help file on the local computer.</span></span> <span data-ttu-id="37ace-260">Ve Windows Powershellu ISE 3.0 a novějších otevře se okno, které obsahuje nápovědu pro rutinu, která je prohledávatelná a je možné konfigurovat.</span><span class="sxs-lookup"><span data-stu-id="37ace-260">In Windows PowerShell ISE 3.0 and later, a window opens that contains the help for the cmdlet that is searchable and configurable.</span></span> <span data-ttu-id="37ace-261">Toto prostředí nápovědy je nová možnost instalace Windows PowerShell ISE 3.0 a aktualizovatelné nápovědy je nová možnost instalace Windows PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="37ace-261">This Help experience is new for Windows PowerShell ISE 3.0, and Updatable Help is new for Windows PowerShell 3.0.</span></span>

### <a name="show-command-cmdlet"></a><span data-ttu-id="37ace-262">Rutiny show-– příkaz</span><span class="sxs-lookup"><span data-stu-id="37ace-262">Show-Command cmdlet</span></span>
<span data-ttu-id="37ace-263">**Přidáno v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="37ace-263">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="37ace-264">**Zobrazit příkaz** rutina umožňuje vytvořit nebo spustit rutiny nebo funkce vyplněním v grafické podobě.</span><span class="sxs-lookup"><span data-stu-id="37ace-264">The **Show-Command** cmdlet enables you to compose or run a cmdlet or function by filling in a graphical form.</span></span> <span data-ttu-id="37ace-265">Formulář umožňuje uživatelům pracovat v prostředí Windows PowerShell v grafickém prostředí.</span><span class="sxs-lookup"><span data-stu-id="37ace-265">The form lets users work with Windows PowerShell in a graphical environment.</span></span> <span data-ttu-id="37ace-266">**Zobrazit příkaz** také umožňuje používat pokročilé autory skriptů k vytvoření rychlého grafického rozhraní pomocí prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37ace-266">**Show-Command** also enables advanced scripters to create a quick Windows PowerShell-based GUI.</span></span>

<span data-ttu-id="37ace-267">**Jakou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="37ace-267">**What value does this change add?**</span></span>

<span data-ttu-id="37ace-268">S použitím **zobrazit příkaz** ve skriptech prostředí Windows PowerShell můžete poskytnout uživatelům grafickém prostředí, ke kterému jsou známé.</span><span class="sxs-lookup"><span data-stu-id="37ace-268">By using **Show-Command** in your Windows PowerShell scripts, you can provide your users with the graphical environment with which they are familiar.</span></span> <span data-ttu-id="37ace-269">**Zobrazit příkaz** může také pomoct úvodní uživatelům naučit se prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37ace-269">**Show-Command** can also help introductory users learn Windows PowerShell.</span></span>

<span data-ttu-id="37ace-270">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="37ace-270">**What works differently?**</span></span>

<span data-ttu-id="37ace-271">Zobrazit příkaz je nový Windows PowerShell ISE 3.0.</span><span class="sxs-lookup"><span data-stu-id="37ace-271">Show-Command is new Windows PowerShell ISE 3.0.</span></span>

## <a name="see-also"></a><span data-ttu-id="37ace-272">Viz taky</span><span class="sxs-lookup"><span data-stu-id="37ace-272">See also</span></span>
<span data-ttu-id="37ace-273">Další informace o používání Windows PowerShell ISE v prostředí Windows PowerShell najdete v následujících tématech.</span><span class="sxs-lookup"><span data-stu-id="37ace-273">For more information about using Windows PowerShell ISE in Windows PowerShell, see the following links.</span></span>

- [<span data-ttu-id="37ace-274">Zkoumání Windows Powershellu Integrované skriptovací prostředí</span><span class="sxs-lookup"><span data-stu-id="37ace-274">Exploring the Windows PowerShell Integrated Scripting Environment</span></span>](../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
- [<span data-ttu-id="37ace-275">ISE na wikiwebu TechNet</span><span class="sxs-lookup"><span data-stu-id="37ace-275">ISE on the TechNet Wiki</span></span>](https://social.technet.microsoft.com/wiki/search/searchresults.aspx?q=ISE)
- [<span data-ttu-id="37ace-276">Centrum skriptů</span><span class="sxs-lookup"><span data-stu-id="37ace-276">Script Center</span></span>](https://technet.microsoft.com/scriptcenter/default)