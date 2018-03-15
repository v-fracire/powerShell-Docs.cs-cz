---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Jaké s 50 powershellu ISE"
ms.assetid: 38648d47-7c27-4b37-a40e-ad29948519c2
ms.openlocfilehash: 9fd25a4759602bebf2b5df2c17d0c816a15e5e2b
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="what39s-new-in-the-windows-powershell-ise"></a><span data-ttu-id="9b4b0-103">Co&#39;s nová funkce v systému Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="9b4b0-103">What&#39;s New in the Windows PowerShell ISE</span></span>
<span data-ttu-id="9b4b0-104">Toto téma popisuje nové a aktualizované funkce, které byly zavedeny ve verzích systému Windows PowerShell Integrované skriptovací prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="9b4b0-104">This topic explains the new and updated features that have been introduced in versions of Windows PowerShell  Integrated Scripting Environment (ISE).</span></span>

## <a name="feature-description"></a><span data-ttu-id="9b4b0-105">Popis funkce</span><span class="sxs-lookup"><span data-stu-id="9b4b0-105">Feature description</span></span>
<span data-ttu-id="9b4b0-106">Windows PowerShell ISE je hostitelskou aplikaci, která umožňuje zápis, spustit a otestovat skriptech a modulech v grafickém uživatelském rozhraní nebo intuitivní prostředí.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-106">The Windows PowerShell ISE is a host application that enables you to write, run, and test scripts and modules in a graphical and intuitive environment.</span></span> <span data-ttu-id="9b4b0-107">Klíčové funkce, jako je například barevné zvýrazňování syntaxe, kartě dokončení, visual ladění, dodržování předpisů kódování Unicode a kontextová nápověda nabízí bohaté skriptovací prostředí.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-107">Key features such as syntax-coloring, tab completion, visual debugging, Unicode compliance, and context-sensitive Help provide a rich scripting experience.</span></span>

<span data-ttu-id="9b4b0-108">Přehled Windows PowerShell ISE najdete v tématu [přehled Windows PowerShell Integrované skriptovací prostředí](https://technet.microsoft.com/library/3c1892c2-bf84-4cb6-af26-1f453be9e671).</span><span class="sxs-lookup"><span data-stu-id="9b4b0-108">For an overview of Windows PowerShell ISE, see [Windows PowerShell Integrated Scripting Environment overview](https://technet.microsoft.com/library/3c1892c2-bf84-4cb6-af26-1f453be9e671).</span></span>

## <a name="new-and-changed-functionality-in-windows-powershell-ise"></a><span data-ttu-id="9b4b0-109">Nové a změněné funkce v systému Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="9b4b0-109">New and changed functionality in Windows PowerShell ISE</span></span>
<span data-ttu-id="9b4b0-110">Následující tabulka uvádí nové a změněné funkce pro tuto verzi systému Windows PowerShell ISE v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-110">The following table lists the new and changed features for this release of Windows PowerShell ISE in Windows PowerShell.</span></span>

|<span data-ttu-id="9b4b0-111">Vlastnost/funkce</span><span class="sxs-lookup"><span data-stu-id="9b4b0-111">Feature/functionality</span></span>|<span data-ttu-id="9b4b0-112">Windows PowerShell ISE 4.0</span><span class="sxs-lookup"><span data-stu-id="9b4b0-112">Windows PowerShell ISE 4.0</span></span>|<span data-ttu-id="9b4b0-113">Windows PowerShell ISE 3.0</span><span class="sxs-lookup"><span data-stu-id="9b4b0-113">Windows PowerShell ISE 3.0</span></span>|<span data-ttu-id="9b4b0-114">Windows PowerShell ISE 2.0</span><span class="sxs-lookup"><span data-stu-id="9b4b0-114">Windows PowerShell ISE 2.0</span></span>|
|--------------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
|<span data-ttu-id="9b4b0-115">**[IntelliSense](#intellisense)**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-115">**[IntelliSense](#intellisense)**</span></span>|<span data-ttu-id="9b4b0-116">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-116">X</span></span>|<span data-ttu-id="9b4b0-117">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-117">X</span></span>||
|<span data-ttu-id="9b4b0-118">**[Fragmenty kódu](#snippets)**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-118">**[Snippets](#snippets)**</span></span>|<span data-ttu-id="9b4b0-119">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-119">X</span></span>|<span data-ttu-id="9b4b0-120">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-120">X</span></span>||
|<span data-ttu-id="9b4b0-121">**[Rozšíření nástrojů](#add-on-tools)**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-121">**[Add-on Tools](#add-on-tools)**</span></span>|<span data-ttu-id="9b4b0-122">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-122">X</span></span>|<span data-ttu-id="9b4b0-123">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-123">X</span></span>||
|<span data-ttu-id="9b4b0-124">**[Správce restartování a automatické ukládání](#restart-manager-and-auto-save)**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-124">**[Restart Manager and Auto-save](#restart-manager-and-auto-save)**</span></span>|<span data-ttu-id="9b4b0-125">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-125">X</span></span>|<span data-ttu-id="9b4b0-126">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-126">X</span></span>||
|<span data-ttu-id="9b4b0-127">**[Seznam naposledy použitých](#most-recently-used-list)**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-127">**[Most-recently used list](#most-recently-used-list)**</span></span>|<span data-ttu-id="9b4b0-128">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-128">X</span></span>|<span data-ttu-id="9b4b0-129">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-129">X</span></span>||
|<span data-ttu-id="9b4b0-130">**[Podokna konzoly](#console-pane)**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-130">**[Console Pane](#console-pane)**</span></span>|<span data-ttu-id="9b4b0-131">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-131">X</span></span>|<span data-ttu-id="9b4b0-132">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-132">X</span></span>||
|<span data-ttu-id="9b4b0-133">**[Přepínače příkazového řádku](#command-line-switches)**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-133">**[Command-line switches](#command-line-switches)**</span></span>|<span data-ttu-id="9b4b0-134">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-134">X</span></span>|<span data-ttu-id="9b4b0-135">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-135">X</span></span>||
|<span data-ttu-id="9b4b0-136">**[Nové funkce editoru](#new-editor-features)**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-136">**[New editor features](#new-editor-features)**</span></span>|<span data-ttu-id="9b4b0-137">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-137">X</span></span>|<span data-ttu-id="9b4b0-138">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-138">X</span></span>||
|<span data-ttu-id="9b4b0-139">**[Nové okna programu Help viewer](#new-help-viewer-window)**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-139">**[New Help viewer window](#new-help-viewer-window)**</span></span>|<span data-ttu-id="9b4b0-140">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-140">X</span></span>|<span data-ttu-id="9b4b0-141">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-141">X</span></span>||
|<span data-ttu-id="9b4b0-142">**[Zobrazit příkaz rutiny](#show-command-cmdlet)**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-142">**[Show-Command cmdlet](#show-command-cmdlet)**</span></span>|<span data-ttu-id="9b4b0-143">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-143">X</span></span>|<span data-ttu-id="9b4b0-144">X</span><span class="sxs-lookup"><span data-stu-id="9b4b0-144">X</span></span>||

### <a name="intellisense"></a><span data-ttu-id="9b4b0-145">IntelliSense</span><span class="sxs-lookup"><span data-stu-id="9b4b0-145">IntelliSense</span></span>
<span data-ttu-id="9b4b0-146">**Přidat v integrovaném Skriptovacím 3.0**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-146">**Added in ISE 3.0**</span></span>

<span data-ttu-id="9b4b0-147">IntelliSense je funkce Automatické dokončování pomoc, která je součástí systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-147">IntelliSense is an automatic-completion assistance feature that is part of Windows PowerShell ISE.</span></span> <span data-ttu-id="9b4b0-148">IntelliSense zobrazí prokliknutelný nabídky potenciálně odpovídajících rutin, parametry, hodnoty parametrů, soubory nebo složky během psaní.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-148">IntelliSense displays clickable menus of potentially matching cmdlets, parameters, parameter values, files, or folders as you type.</span></span>

<span data-ttu-id="9b4b0-149">**Jakou přidanou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-149">**What value does this change add?**</span></span>

<span data-ttu-id="9b4b0-150">Po přidání IntelliSense je jednodušší zjistit rutiny a syntaxe při použití Windows PowerShell ISE vytvořit skripty.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-150">With the addition of IntelliSense, it is easier to discover cmdlets and syntax when you use Windows PowerShell ISE to create scripts.</span></span> <span data-ttu-id="9b4b0-151">Windows PowerShell ISE můžete použít také další prostředí Windows PowerShell při vytváření nové skripty.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-151">You can also use Windows PowerShell ISE to learn Windows PowerShell while you create new scripts.</span></span>

<span data-ttu-id="9b4b0-152">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-152">**What works differently?**</span></span>

<span data-ttu-id="9b4b0-153">Když zadáte rutiny Windows PowerShell ISE 3.0 nebo novější, zobrazí nabídky posouvatelného a můžete kliknout, umožní vám procházet a vyberte příslušné příkazy.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-153">When you type cmdlets in the Windows PowerShell ISE 3.0 or later, a scrollable and clickable menu displays, allowing you to browse and select the appropriate commands.</span></span>

### <a name="snippets"></a><span data-ttu-id="9b4b0-154">Fragmenty kódu</span><span class="sxs-lookup"><span data-stu-id="9b4b0-154">Snippets</span></span>
<span data-ttu-id="9b4b0-155">**Přidat v integrovaném Skriptovacím 3.0**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-155">**Added in ISE 3.0**</span></span>

<span data-ttu-id="9b4b0-156">*Fragmenty kódu* krátké části kód prostředí Windows PowerShell, který můžete vložit do skriptů, které vytvoříte v systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-156">*Snippets* are short sections of Windows PowerShell code that you can insert into the scripts you create in Windows PowerShell ISE.</span></span> <span data-ttu-id="9b4b0-157">Windows PowerShell ISE se dodává s výchozí sadu fragmenty kódu.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-157">Windows PowerShell ISE comes with a default set of snippets.</span></span> <span data-ttu-id="9b4b0-158">Fragmenty kódu můžete přidat pomocí **New-fragment** rutiny při práci s Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-158">You can add snippets by using the **New-Snippet** cmdlet while working in Windows PowerShell ISE.</span></span>

<span data-ttu-id="9b4b0-159">**Jakou přidanou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-159">**What value does this change add?**</span></span>

<span data-ttu-id="9b4b0-160">Pomocí fragmenty kódu můžete rychle sestavit a vytvářet skripty pro automatizaci prostředí.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-160">By using snippets, you can quickly assemble and create scripts to automate your environment.</span></span>

<span data-ttu-id="9b4b0-161">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-161">**What works differently?**</span></span>

<span data-ttu-id="9b4b0-162">Na použití fragmenty kódu v prostředí Windows PowerShell 3.0 nebo novější, **upravit** nabídky, klikněte na **spustit fragmenty**, nebo stiskněte klávesu **Ctrl-J**.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-162">To use snippets in Windows PowerShell 3.0 or later, on the **Edit** menu, click **Start Snippets**, or press **Ctrl-J**.</span></span>

### <a name="add-on-tools"></a><span data-ttu-id="9b4b0-163">Rozšíření nástrojů</span><span class="sxs-lookup"><span data-stu-id="9b4b0-163">Add-on tools</span></span>
<span data-ttu-id="9b4b0-164">**Přidat v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-164">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="9b4b0-165">Windows PowerShell ISE teď podporuje rozšíření nástroje, které jsou ovládací prvky Windows Presentation Foundation (WPF), které jsou přidané pomocí objektového modelu.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-165">Windows PowerShell ISE now supports add-on tools, which are Windows Presentation Foundation (WPF) controls that are added by using the object model.</span></span> <span data-ttu-id="9b4b0-166">Doplněk nástroje lze zobrazit jako svislé nebo vodorovné podokno v konzole.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-166">Add-on tools can be displayed as a vertical or horizontal pane in the console.</span></span> <span data-ttu-id="9b4b0-167">Několik rozšíření nástrojů v podokně se zobrazí jako záložkách ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-167">Multiple add-on tools in a pane are displayed as a tabbed control.</span></span> <span data-ttu-id="9b4b0-168">Můžete také přidat nebo odebrat nástroje doplňků, které vytváří strany jiných společností než Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-168">You can also add or remove add-on tools that are produced by non-Microsoft parties.</span></span> <span data-ttu-id="9b4b0-169">Další informace o tom, jak importovat nebo odebrání nástrojů pro rozšíření najdete v tématu [operace systému Windows PowerShell ISE](http://technet.microsoft.com/library/cc732148.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b4b0-169">For more information about how to import or remove add-on tools, see [Windows PowerShell ISE Operations](http://technet.microsoft.com/library/cc732148.aspx).</span></span>

<span data-ttu-id="9b4b0-170">**Jakou přidanou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-170">**What value does this change add?**</span></span>

<span data-ttu-id="9b4b0-171">Rozšíření umožňují rozšířit a přizpůsobit Windows PowerShell ISE s nástroji, které mohou rozšířit možnosti skriptování nebo přidání funkcí do systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-171">Add-ons allow you to extend and customize Windows PowerShell ISE with tools that can enhance your scripting experience or add functionality to Windows PowerShell ISE.</span></span>

<span data-ttu-id="9b4b0-172">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-172">**What works differently?**</span></span>

<span data-ttu-id="9b4b0-173">Prostředí Windows PowerShell ISE 3.0 a novějších jsou součástí **příkazy** rozšíření.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-173">Windows PowerShell ISE 3.0 and later come with the **Commands** add-on.</span></span> <span data-ttu-id="9b4b0-174">**Příkazy** rozšíření umožňuje procházet rutiny a získat přístup k nápovědě o rutiny-souběžného s **skriptu** a **konzoly** podokna.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-174">The **Commands** add-on allows you to browse cmdlets, and access help about the cmdlets side-by-side with the **Script** and **Console** Panes.</span></span>

<span data-ttu-id="9b4b0-175">Další doplňky můžete najít pomocí **otevřete doplněk Nástroje pro web** příkazu na **doplňky** nabídky.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-175">Additional add-ons can be found by using the **Open Add-on Tools Website** command on the **Add-ons** menu.</span></span>

### <a name="restart-manager-and-auto-save"></a><span data-ttu-id="9b4b0-176">Restartujte manager a automatické ukládání</span><span class="sxs-lookup"><span data-stu-id="9b4b0-176">Restart manager and auto-save</span></span>
<span data-ttu-id="9b4b0-177">**Přidat v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-177">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="9b4b0-178">Windows PowerShell ISE nyní automaticky uloží otevřete skripty každé dvě minuty, v samostatných umístění.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-178">Windows PowerShell ISE now automatically saves your open scripts every two minutes, in a separate location.</span></span>  <span data-ttu-id="9b4b0-179">Pokud Windows PowerShell ISE přestane fungovat, nebo pokud je restartován operační systém, po restartování prostředí Windows PowerShell ISE, obnoví otevřete skripty, které byly v průběhu poslední relace, i v případě, že tyto skripty nebyly uloženy.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-179">If Windows PowerShell ISE stops working, or if the operating system is restarted, after Windows PowerShell ISE restarts, it recovers scripts that were open in the last session, even if the scripts were not saved.</span></span>

<span data-ttu-id="9b4b0-180">Pokud chcete změnit interval automatické ukládání, spusťte následující příkaz v podokně konzoly: **$psise. Options.AutoSaveMinuteInterval**.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-180">To change the automatic saving interval, run the following command in the Console pane: **$psise.Options.AutoSaveMinuteInterval**.</span></span>

<span data-ttu-id="9b4b0-181">**Jakou přidanou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-181">**What value does this change add?**</span></span>

<span data-ttu-id="9b4b0-182">Teď můžete pracovat v rámci systému Windows PowerShell ISE zároveň budete vědět, že otevřete skripty automaticky uloží v případě neočekávaného restartování.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-182">You can now work within Windows PowerShell ISE knowing that your open scripts are automatically saved in the event of an unexpected restart.</span></span>

<span data-ttu-id="9b4b0-183">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-183">**What works differently?**</span></span>

<span data-ttu-id="9b4b0-184">Prostředí Windows PowerShell ISE 2.0 neuloží skripty automaticky v případě restartování.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-184">Windows PowerShell ISE 2.0 does not save the scripts automatically in the event of a restart.</span></span>

### <a name="most-recently-used-list"></a><span data-ttu-id="9b4b0-185">Seznam naposledy použitých</span><span class="sxs-lookup"><span data-stu-id="9b4b0-185">Most-recently used list</span></span>
<span data-ttu-id="9b4b0-186">**Přidat v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-186">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="9b4b0-187">Windows PowerShell ISE teď obsahuje seznam naposledy použitých souborů.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-187">Windows PowerShell ISE now has a most-recently used list for files.</span></span> <span data-ttu-id="9b4b0-188">Při otevření souboru v systému Windows PowerShell ISE, soubor je přidaný do seznamu naposledy použitých na **souboru** nabídky.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-188">When you open a file in Windows PowerShell ISE, the file is added to the most-recently used list on the **File** menu.</span></span>

<span data-ttu-id="9b4b0-189">Chcete-li změnit výchozí počet souborů v seznamu naposledy použitých, spusťte následující příkaz v podokně konzoly: **$psise. Options.MruCount**.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-189">To change the default number of files in the most-recently used list, run the following command in the Console Pane: **$psise.Options.MruCount**.</span></span>

<span data-ttu-id="9b4b0-190">**Jakou přidanou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-190">**What value does this change add?**</span></span>

<span data-ttu-id="9b4b0-191">Seznam naposledy použitých teď můžete snadno přístup k souborům se často používá.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-191">You can now use the most-recently used list to easily access your frequently-used files.</span></span>

<span data-ttu-id="9b4b0-192">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-192">**What works differently?**</span></span>

<span data-ttu-id="9b4b0-193">Prostředí Windows PowerShell ISE 2.0 nemá seznam naposledy použitých.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-193">Windows PowerShell ISE 2.0 does not have a most-recently used list.</span></span>

### <a name="console-pane"></a><span data-ttu-id="9b4b0-194">Podokna konzoly</span><span class="sxs-lookup"><span data-stu-id="9b4b0-194">Console Pane</span></span>
<span data-ttu-id="9b4b0-195">**Přidat v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-195">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="9b4b0-196">Samostatný příkaz i jeho podokna výstup, které byly dostupné v první verzi systému Windows PowerShell ISE sloučeny do jednoho podokna konzoly.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-196">The separate Command and Output Panes that were available in the first release of Windows PowerShell ISE have been combined into a single Console Pane.</span></span> <span data-ttu-id="9b4b0-197">V podokně konzoly je podobné funkce a vzhled typické konzoly prostředí Windows PowerShell, ale obsahuje následující vylepšení (většina jsou popsány v tomto tématu).</span><span class="sxs-lookup"><span data-stu-id="9b4b0-197">The Console Pane is similar in function and appearance to a typical Windows PowerShell console, but it includes the following enhancements (most are described in this topic).</span></span>

- <span data-ttu-id="9b4b0-198">Barevné zvýrazňování syntaxe pro vstupní text (není výstup text), včetně syntaxe jazyka XML</span><span class="sxs-lookup"><span data-stu-id="9b4b0-198">Syntax coloring for input text (not output text), including XML syntax</span></span>

- <span data-ttu-id="9b4b0-199">IntelliSense</span><span class="sxs-lookup"><span data-stu-id="9b4b0-199">IntelliSense</span></span>

- <span data-ttu-id="9b4b0-200">Související závorky</span><span class="sxs-lookup"><span data-stu-id="9b4b0-200">Brace matching</span></span>

- <span data-ttu-id="9b4b0-201">Označení chyb</span><span class="sxs-lookup"><span data-stu-id="9b4b0-201">Error indication</span></span>

- <span data-ttu-id="9b4b0-202">Plná podpora Unicode</span><span class="sxs-lookup"><span data-stu-id="9b4b0-202">Full Unicode support</span></span>

- <span data-ttu-id="9b4b0-203">**F1** Kontextová nápověda</span><span class="sxs-lookup"><span data-stu-id="9b4b0-203">**F1** context-sensitive help</span></span>

- <span data-ttu-id="9b4b0-204">**CTRL + F1** kontextová zobrazit – příkaz</span><span class="sxs-lookup"><span data-stu-id="9b4b0-204">**Ctrl+F1** context-sensitive Show-Command</span></span>

- <span data-ttu-id="9b4b0-205">Komplexní skript a podpora zprava doleva</span><span class="sxs-lookup"><span data-stu-id="9b4b0-205">Complex script and right-to-left support</span></span>

- <span data-ttu-id="9b4b0-206">Podpora písma</span><span class="sxs-lookup"><span data-stu-id="9b4b0-206">Font support</span></span>

- <span data-ttu-id="9b4b0-207">Přiblížení</span><span class="sxs-lookup"><span data-stu-id="9b4b0-207">Zoom</span></span>

- <span data-ttu-id="9b4b0-208">Režimy řádku – vybrat a vyberte bloku</span><span class="sxs-lookup"><span data-stu-id="9b4b0-208">Line-select and block-select modes</span></span>

- <span data-ttu-id="9b4b0-209">Písmen a zachovávání s typem obsahu na příkazovém řádku při stisknutí volby **až** šipku zobrazení historie v konzole</span><span class="sxs-lookup"><span data-stu-id="9b4b0-209">Preservation of typed content at the command line when you press the **Up** arrow to view history in the console</span></span>

<span data-ttu-id="9b4b0-210">**Jakou přidanou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-210">**What value does this change add?**</span></span>

<span data-ttu-id="9b4b0-211">Přidání těchto změn podokna konzoly poskytuje skriptovací prostředí, které je konzistentní s rozhraní konzoly.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-211">The addition of these Console Pane changes provides a scripting experience that is more consistent with the console interface.</span></span>

<span data-ttu-id="9b4b0-212">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-212">**What works differently?**</span></span>

<span data-ttu-id="9b4b0-213">Prostředí Windows PowerShell ISE 2.0 má samostatný příkaz a výstupní podokna.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-213">Windows PowerShell ISE 2.0 has separate Command and Output Panes.</span></span>

### <a name="command-line-switches"></a><span data-ttu-id="9b4b0-214">Přepínače příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="9b4b0-214">Command-line switches</span></span>
<span data-ttu-id="9b4b0-215">**Přidat v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-215">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="9b4b0-216">Pokud spustíte z příkazového řádku Windows PowerShell ISE (zadáním **powershell_ise.exe**), můžete přidat následující nové přepínače příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-216">If you start Windows PowerShell ISE from the command line (by typing **powershell_ise.exe**), you can add the following new command-line switches.</span></span>

- <span data-ttu-id="9b4b0-217">*-NoProfile*: spuštění systému Windows PowerShell ISE bez nutnosti spustit **$profile**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-217">*-NoProfile*: Starts Windows PowerShell ISE without running **$profile**</span></span>

- <span data-ttu-id="9b4b0-218">*-Help*: Zobrazí okno nápovědy</span><span class="sxs-lookup"><span data-stu-id="9b4b0-218">*-Help*: Displays a Help window</span></span>

- <span data-ttu-id="9b4b0-219">*-mta*: spustí ISE Windows PowerShell v režimu více vláken typu apartment.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-219">*-mta*: Starts Windows PowerShell ISE in multithreaded apartment mode.</span></span> <span data-ttu-id="9b4b0-220">Single-threaded apartment režimu, je výchozí režim operace pro Windows PowerShell ISE nebo *- sta*.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-220">The default operation mode for Windows PowerShell ISE is single-threaded apartment mode, or *-sta*.</span></span>

<span data-ttu-id="9b4b0-221">**Jakou přidanou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-221">**What value does this change add?**</span></span>

<span data-ttu-id="9b4b0-222">Přidání tyto přepínače příkazového řádku umožňuje řídit prostředí, ve kterém se spouští Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-222">The addition of these command-line switches allows you to control the environment in which the Windows PowerShell ISE runs.</span></span>

<span data-ttu-id="9b4b0-223">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-223">**What works differently?**</span></span>

<span data-ttu-id="9b4b0-224">Prostředí Windows PowerShell ISE 2.0 nerozpoznal tyto přepínače příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-224">Windows PowerShell ISE 2.0 does not recognize these command-line switches.</span></span>

### <a name="new-editor-features"></a><span data-ttu-id="9b4b0-225">Nové funkce editoru</span><span class="sxs-lookup"><span data-stu-id="9b4b0-225">New editor features</span></span>
<span data-ttu-id="9b4b0-226">**Přidat v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-226">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="9b4b0-227">Další úpravy funkce systému Windows PowerShell ISE zahrnují:</span><span class="sxs-lookup"><span data-stu-id="9b4b0-227">Other Windows PowerShell ISE editing features include:</span></span>

- <span data-ttu-id="9b4b0-228">**Barevné zvýrazňování syntaxe XML**Windows PowerShell ISE teď barvy syntaxe jazyka XML stejným způsobem, jak ho barvy syntaxe prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-228">**XML syntax coloring**Windows PowerShell ISE now colors XML syntax in the same way as it colors Windows PowerShell syntax.</span></span>

- <span data-ttu-id="9b4b0-229">**Odpovídající složené závorce** Windows PowerShell ISE obsahuje odpovídající složené závorce a zvýraznění a je možné následujícím způsobem: (například pomocí **přejděte tak, aby shodu** příkaz nebo **Ctrl +]** vyhledá uzavírací závorku, pokud máte složená závorka vybrané).</span><span class="sxs-lookup"><span data-stu-id="9b4b0-229">**Brace matching** Windows PowerShell ISE includes brace matching and highlighting, and can be used in the following ways: (for example, using the **Go to Match** command or **Ctrl + ]** locates the closing brace, if you have an opening brace selected).</span></span>

- <span data-ttu-id="9b4b0-230">**Zobrazení osnovy** podokně skriptu podporuje osnovy, což umožňuje sbalení nebo rozbalení sekcí kódu kliknutím plus nebo minus přihlásí levým okrajem.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-230">**Outline view** The Script Pane supports outlining, which allows collapsing or expanding sections of code by clicking plus or minus signs in the left margin.</span></span> <span data-ttu-id="9b4b0-231">Můžete použít složené závorky nebo **#region** a **#endregion** značky k označení začátku nebo konci sbalitelné části.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-231">You can use braces or the **#region** and **#endregion** tags to mark the beginning or end of a collapsible section.</span></span> <span data-ttu-id="9b4b0-232">Chcete-li rozbalit nebo sbalit všechny oblasti, stiskněte **kombinaci kláves Ctrl + M**.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-232">To expand or collapse all regions, press **Ctrl + M**.</span></span>

- <span data-ttu-id="9b4b0-233">**Přetáhnout myší úpravy textu**ISE Windows PowerShell teď podporuje přetažení úpravy textu.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-233">**Drag and drop text editing**Windows PowerShell ISE now supports drag and drop text editing.</span></span> <span data-ttu-id="9b4b0-234">Můžete vybrat všechny blok textu a přetáhněte tento text do jiného umístění v editoru nebo konzole přesunout text.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-234">You can select any block of text and drag that text to another location in the editor or the console to move the text.</span></span> <span data-ttu-id="9b4b0-235">Pokud podržíte stisknutou klávesu Ctrl a přetáhněte vybraný text po uvolnění tlačítka myši text zkopírován do nového umístění.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-235">If you hold down the Ctrl key while you drag the selected text, when you release the mouse button the text is copied to the new location.</span></span> <span data-ttu-id="9b4b0-236">V této verzi systému Windows PowerShell ISE, jakož i předchozí verzi systému Windows PowerShell ISE když jste přetažení soubory do systému Windows PowerShell ISE Windows PowerShell ISE otevře soubor.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-236">In this version of Windows PowerShell ISE, as well as the previous version of Windows PowerShell ISE, when you drag and drop files onto Windows PowerShell ISE, Windows PowerShell ISE opens the file.</span></span>

- <span data-ttu-id="9b4b0-237">**Analýza chybových zpráv** analýzy chyby jsou označeny červenou podtržení.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-237">**Parse error display** Parse errors are indicated with red underlines.</span></span> <span data-ttu-id="9b4b0-238">Po přesunutí ukazatele myši uvedené chyby, zobrazí se text popisku problém, který nebyl nalezen v kódu.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-238">When you hover over an indicated error, tooltip text displays the problem that was found in the code.</span></span>

- <span data-ttu-id="9b4b0-239">**Zvětšení** procento přiblížení konzoly '™ s obsahu lze nastavit pomocí posuvníku přiblížení (v pravém dolním rohu okna Windows PowerShell ISE) nebo zadáním příkazu **$psise.options.Zoom** v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-239">**Zoom** The zoom percentage of the console'™s content can be set by using the zoom slider (in the lower right corner of Windows PowerShell ISE window), or by entering the command **$psise.options.Zoom** in the Console Pane.</span></span>

- <span data-ttu-id="9b4b0-240">**Rich text zkopírovat a vložit** kopírování do schránky v systému Windows PowerShell ISE uchovává písma, velikosti a barvy informace původní výběru.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-240">**Rich text copy and paste** Copying to the clipboard in Windows PowerShell ISE preserves the font, size, and color information of the original selection.</span></span>

- <span data-ttu-id="9b4b0-241">**Blokovat výběr** blok textu můžete vybrat, podržte klávesu ALT a výběr textu v podokně skriptu s myší nebo stisknutím klávesy **Alt + Shift + šipka**.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-241">**Block selection** You can select a block of text by holding down the ALT key while selecting text in the Script Pane with your mouse, or by pressing **Alt+Shift+Arrow**.</span></span>

<span data-ttu-id="9b4b0-242">**Jakou přidanou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-242">**What value does this change add?**</span></span>

<span data-ttu-id="9b4b0-243">Další úpravy funkce poskytují více konzistentní a efektivní prostředí pro úpravy.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-243">The additional editing features provide a more consistent and powerful editing environment.</span></span>

<span data-ttu-id="9b4b0-244">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-244">**What works differently?**</span></span>

<span data-ttu-id="9b4b0-245">Tyto úpravy vylepšení nebyly nalezeny v prostředí Windows PowerShell ISE 2.0.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-245">These editing enhancements were not present in Windows PowerShell ISE 2.0.</span></span>

### <a name="new-help-viewer-window"></a><span data-ttu-id="9b4b0-246">Nové okna programu Help viewer</span><span class="sxs-lookup"><span data-stu-id="9b4b0-246">New Help viewer window</span></span>
<span data-ttu-id="9b4b0-247">**Přidat v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-247">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="9b4b0-248">Pokud vyberete **F1** Pokud vaše kurzor se nachází v rutiny, nebo máte součástí rutiny zvýrazněná, nový prohlížeč nápovědy otevře kontextové nápovědy o rutině zvýrazněné.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-248">If you press **F1** when your cursor is in a cmdlet, or you have part of a cmdlet highlighted, the new Help viewer opens context-sensitive Help about the highlighted cmdlet.</span></span> <span data-ttu-id="9b4b0-249">Chcete-li zobrazit nápovědu Windows PowerShell o, zadejte **operátory** v podokně konzoly a poté stiskněte klávesu **F1**.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-249">To display Windows PowerShell About help, type  **operators** in the console pane, and then press **F1**.</span></span>

<span data-ttu-id="9b4b0-250">Před použitím této funkce stažení nejnovější verze témat nápovědy prostředí Windows PowerShell na webu společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-250">Before you use this feature, download the most current version of Windows PowerShell Help topics from the Microsoft website.</span></span> <span data-ttu-id="9b4b0-251">Nejjednodušší způsob stahování témata nápovědy je spuštění **Update-Help** rutiny v podokně konzoly při spuštění Windows PowerShell ISE jako správce.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-251">The simplest method for downloading the Help topics is to run the **Update-Help** cmdlet in the Console Pane when running Windows PowerShell ISE as administrator.</span></span>

<span data-ttu-id="9b4b0-252">Kde můžete změnit **F1** klíč hledá nápovědy.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-252">You can alter where the **F1** key looks for Help.</span></span> <span data-ttu-id="9b4b0-253">V **nástroje**/**možnosti** nabídky na **obecné nastavení** v části **další nastavení**, můžete nastavit nebo vymazat zaškrtávací políčko **používat místní obsah nápovědy místo obsahu online**.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-253">In the **Tools**/**Options** menu, on the **General Settings** tab, under **Other Settings**, you can set or clear the checkbox **Use local help content instead of online content**.</span></span> <span data-ttu-id="9b4b0-254">Pokud je zaškrtnuto, pak klient vyhledá rutinu Nápověda v nápovědě stažené nachází ve složce moduly.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-254">If checked, then the client looks for the cmdlet Help in the downloaded Help found in the modules folder.</span></span>  <span data-ttu-id="9b4b0-255">Pokud není políčko zaškrtnuto, klient Hledat na nápovědu rutiny v knihovně TechNet.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-255">If the checkbox is cleared, then the client looks on the TechNet library for the cmdlet help.</span></span>

<span data-ttu-id="9b4b0-256">**Jakou přidanou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-256">**What value does this change add?**</span></span>

<span data-ttu-id="9b4b0-257">Kontextová nápověda, aniž byste museli opustit váš aktuální rutiny nebo skriptu zajišťuje bezproblémové learning prostředí.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-257">Context-sensitive Help without leaving your current cmdlet or script provides a seamless learning experience.</span></span>

<span data-ttu-id="9b4b0-258">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-258">**What works differently?**</span></span>

<span data-ttu-id="9b4b0-259">Stisknutím klávesy F1 v předchozích verzích systému Windows PowerShell ISE otevřít soubor nápovědy v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-259">Pressing F1 in previous versions of Windows PowerShell ISE opened the help file on the local computer.</span></span> <span data-ttu-id="9b4b0-260">V prostředí Windows PowerShell ISE 3.0 nebo novější otevře se okno obsahující nápovědu pro rutinu, která je s možností vyhledávání a konfigurovat.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-260">In Windows PowerShell ISE 3.0 and later, a window opens that contains the help for the cmdlet that is searchable and configurable.</span></span> <span data-ttu-id="9b4b0-261">Toto prostředí nápovědy je nového pro prostředí Windows PowerShell ISE 3.0 a aktualizovatelné nápovědy je nového pro prostředí Windows PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-261">This Help experience is new for Windows PowerShell ISE 3.0, and Updatable Help is new for Windows PowerShell 3.0.</span></span>

### <a name="show-command-cmdlet"></a><span data-ttu-id="9b4b0-262">Zobrazit příkaz rutiny</span><span class="sxs-lookup"><span data-stu-id="9b4b0-262">Show-Command cmdlet</span></span>
<span data-ttu-id="9b4b0-263">**Přidat v prostředí PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-263">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="9b4b0-264">**Zobrazit příkaz** rutina umožňuje vytvořit nebo spouštět rutiny nebo funkce vyplněním grafických formulářů.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-264">The **Show-Command** cmdlet enables you to compose or run a cmdlet or function by filling in a graphical form.</span></span> <span data-ttu-id="9b4b0-265">Formulář umožňuje uživatelům práci s prostředím Windows PowerShell v grafickém prostředí.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-265">The form lets users work with Windows PowerShell in a graphical environment.</span></span> <span data-ttu-id="9b4b0-266">**Zobrazit příkaz** také umožňuje pokročilé autory skriptů vytvořit rychlé grafického rozhraní založené na prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-266">**Show-Command** also enables advanced scripters to create a quick Windows PowerShell-based GUI.</span></span>

<span data-ttu-id="9b4b0-267">**Jakou přidanou hodnotu tato změna přináší?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-267">**What value does this change add?**</span></span>

<span data-ttu-id="9b4b0-268">Pomocí **zobrazit příkaz** v prostředí Windows PowerShell skripty, můžete poskytnout uživatelům grafické prostředí, ke kterému jsou známé.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-268">By using **Show-Command** in your Windows PowerShell scripts, you can provide your users with the graphical environment with which they are familiar.</span></span> <span data-ttu-id="9b4b0-269">**Zobrazit příkaz** může také pomoci úvodní uživatelé další prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-269">**Show-Command** can also help introductory users learn Windows PowerShell.</span></span>

<span data-ttu-id="9b4b0-270">**Co funguje jinak?**</span><span class="sxs-lookup"><span data-stu-id="9b4b0-270">**What works differently?**</span></span>

<span data-ttu-id="9b4b0-271">Zobrazit příkaz je nové prostředí Windows PowerShell ISE 3.0.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-271">Show-Command is new Windows PowerShell ISE 3.0.</span></span>

## <a name="see-also"></a><span data-ttu-id="9b4b0-272">Viz taky</span><span class="sxs-lookup"><span data-stu-id="9b4b0-272">See also</span></span>
<span data-ttu-id="9b4b0-273">Další informace o používání v prostředí Windows PowerShell Windows PowerShell ISE najdete v následujících tématech.</span><span class="sxs-lookup"><span data-stu-id="9b4b0-273">For more information about using Windows PowerShell ISE in Windows PowerShell, see the following links.</span></span>

- [<span data-ttu-id="9b4b0-274">Zkoumání Windows PowerShell Integrované skriptovací prostředí</span><span class="sxs-lookup"><span data-stu-id="9b4b0-274">Exploring the Windows PowerShell Integrated Scripting Environment</span></span>](../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
- [<span data-ttu-id="9b4b0-275">ISE na webu TechNet Wiki</span><span class="sxs-lookup"><span data-stu-id="9b4b0-275">ISE on the TechNet Wiki</span></span>](http://social.technet.microsoft.com/wiki/search/searchresults.aspx?q=ISE)
- [<span data-ttu-id="9b4b0-276">Centra skriptů</span><span class="sxs-lookup"><span data-stu-id="9b4b0-276">Script Center</span></span>](http://technet.microsoft.com/scriptcenter/default)

