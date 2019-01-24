---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Integrované skriptovací prostředí ISE Windows Powershellu
ms.assetid: f156b92d-0203-46d2-89c7-b4989d32e3d2
ms.openlocfilehash: a5fcc8c813349d0b85cc3af29047424fe787d168
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403633"
---
# <a name="windows-powershell-integrated-scripting-environment-ise"></a><span data-ttu-id="1c2de-103">Integrované skriptovací prostředí (ISE) v prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c2de-103">Windows PowerShell Integrated Scripting Environment (ISE)</span></span>

<span data-ttu-id="1c2de-104">Windows Powershellu integrovaném skriptovacím prostředí (ISE) je mezi dvěma hostiteli pro modul prostředí Windows PowerShell a jazyk.</span><span class="sxs-lookup"><span data-stu-id="1c2de-104">The Windows PowerShell Integrated Scripting Environment (ISE) is one of two hosts for the Windows PowerShell engine and language.</span></span> <span data-ttu-id="1c2de-105">S ní můžete zapisovat, spouštět a testovat skripty způsoby, které nejsou k dispozici v konzole Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="1c2de-105">With it you can write, run, and test scripts in ways that are not available in the Windows PowerShell Console.</span></span> <span data-ttu-id="1c2de-106">ISE přidá barevné zvýrazňování syntaxe, dokončování pomocí tabulátoru, technologie IntelliSense, ladění visual a kontextové nápovědy.</span><span class="sxs-lookup"><span data-stu-id="1c2de-106">The ISE adds syntax-coloring, tab completion, IntelliSense, visual debugging, and context sensitive Help.</span></span>

<span data-ttu-id="1c2de-107">ISE umožňuje spouštění příkazů v podokně konzoly, ale také podporuje podoken, které můžete použít současně zobrazit zdrojový kód skriptu a dalších nástrojů, které se můžete zapojit do ISE.</span><span class="sxs-lookup"><span data-stu-id="1c2de-107">The ISE lets you run commands in a console pane, but it also supports panes that you can use to simultaneously view the source code of your script and other tools that can plug into the ISE.</span></span> <span data-ttu-id="1c2de-108">Ve stejnou dobu, což je zvláště užitečné při ladění skriptu, který používá funkce definované v jiné skripty a moduly můžete otevřít i více skriptů windows.</span><span class="sxs-lookup"><span data-stu-id="1c2de-108">You can even open up multiple script windows at the same time, which is especially helpful when you are debugging a script that uses functions defined in other scripts or modules.</span></span>

## <a name="whats-new"></a><span data-ttu-id="1c2de-109">Co je nového</span><span class="sxs-lookup"><span data-stu-id="1c2de-109">What’s New</span></span>

<span data-ttu-id="1c2de-110">Tady jsou některé funkce, které byly přidány do nejnovější verze prostředí PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="1c2de-110">Here are some of the features that have been added to the ISE in the most recent releases of PowerShell.</span></span>

### <a name="added-in-powershell-30-windows-server-2012-windows-8"></a><span data-ttu-id="1c2de-111">Přidáno v prostředí PowerShell 3.0 (Windows Server 2012, Windows 8)</span><span class="sxs-lookup"><span data-stu-id="1c2de-111">Added in PowerShell 3.0 (Windows Server 2012, Windows 8)</span></span>

<span data-ttu-id="1c2de-112">**Technologie IntelliSense** zobrazením nabídky odpovídající rutiny, parametry, hodnoty parametrů, soubory nebo složky při psaní automaticky dokončí příkazům.</span><span class="sxs-lookup"><span data-stu-id="1c2de-112">**IntelliSense** automatically completes your commands by displaying menus of matching cmdlets, parameters, parameter values, files, or folders as you type.</span></span>

<span data-ttu-id="1c2de-113">**Fragmenty kódu** jsou krátké části kódu, můžete jednoduše vložit do skriptů vaše zápisu.</span><span class="sxs-lookup"><span data-stu-id="1c2de-113">**Snippets** are short sections of code that you can easily insert into the scripts your write.</span></span> <span data-ttu-id="1c2de-114">Kolekce užitečné fragmentů kódu je součástí pole a je možné pomocí více **New-fragment** rutiny.</span><span class="sxs-lookup"><span data-stu-id="1c2de-114">A collection of useful snippets is included in the box and you can more by using the **New-Snippet** cmdlet.</span></span>

<span data-ttu-id="1c2de-115">**Doplňkové nástroje** přidá funkce, které chcete ISE mohou vytvořit psaní kódu, který komunikuje s [The Windows Powershellu objektový Model skriptování ISE](../../core-powershell/ise/The-ISE-Object-Model-Hierarchy.md).</span><span class="sxs-lookup"><span data-stu-id="1c2de-115">**Add-on tools** that add features to the ISE can be created by writing code that interacts with [The Windows PowerShell ISE Scripting Object Model](../../core-powershell/ise/The-ISE-Object-Model-Hierarchy.md).</span></span>

<span data-ttu-id="1c2de-116">Tyto nástroje můžete zobrazit ovládací prvky v podokně s kartami nebo transparentně pracovat na pozadí.</span><span class="sxs-lookup"><span data-stu-id="1c2de-116">These tools can display controls in a tabbed pane or work invisibly in the background.</span></span> <span data-ttu-id="1c2de-117">**Příkazy** doplněk je typickým příkladem a je součástí verze 3.0 a novější, který zobrazí seznam dostupných příkazů a jejich nápovědy.</span><span class="sxs-lookup"><span data-stu-id="1c2de-117">The **Commands** add-on is a good example and is included with version 3.0 and later that displays a list of the available commands and their Help.</span></span>

<span data-ttu-id="1c2de-118">**Restartovat správce a automatického ukládání** automaticky uloží vaše skripty každé dvě minuty abyste se vyhnuli ztrátě práce v případě chyb nebo neočekávaného restartování.</span><span class="sxs-lookup"><span data-stu-id="1c2de-118">**Restart Manager and Auto-save** automatically save your scripts every two minutes to help you avoid the loss of your work in the event of a crash or unexpected restart.</span></span>

<span data-ttu-id="1c2de-119">**Seznam naposledy použitých nejčastěji** je teď součástí souboru otevřít nabídku, aby bylo snazší získat soubory, které použijete nejčastěji.</span><span class="sxs-lookup"><span data-stu-id="1c2de-119">**Most Recently Used list** is now part of the File Open menu to make it easier to get to the files you use most often.</span></span>

<span data-ttu-id="1c2de-120">**Sloučené podokně konzoly**.</span><span class="sxs-lookup"><span data-stu-id="1c2de-120">**Merged Console pane**.</span></span> <span data-ttu-id="1c2de-121">V předchozích verzích ISE byly samostatný příkaz a výstupní podokna.</span><span class="sxs-lookup"><span data-stu-id="1c2de-121">In previous versions of the ISE there were separate Command and Output panes.</span></span> <span data-ttu-id="1c2de-122">Jsou nyní zkombinovány do jediného, že informace přímo napodobuje uvidíte v konzole Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="1c2de-122">They are now combined into a single pane that more directly mimics what you see in the Windows Powershell Console.</span></span>

<span data-ttu-id="1c2de-123">**Přepínače příkazového řádku**.</span><span class="sxs-lookup"><span data-stu-id="1c2de-123">**Command-line switches**.</span></span> <span data-ttu-id="1c2de-124">Několik nových přepínače příkazového řádku získáte větší kontrolu nad tím, jak funguje ISE.</span><span class="sxs-lookup"><span data-stu-id="1c2de-124">Several new command-line switches give you more control over the way the ISE works.</span></span> <span data-ttu-id="1c2de-125">-NoProfile spustí ISE bez spuštění skriptu profilu.</span><span class="sxs-lookup"><span data-stu-id="1c2de-125">-NoProfile starts the ISE without running a profile script.</span></span> <span data-ttu-id="1c2de-126">-Help otevře se okno nápovědy s ISE.</span><span class="sxs-lookup"><span data-stu-id="1c2de-126">-Help opens up a help window with the ISE.</span></span> <span data-ttu-id="1c2de-127">-mta spustí ISE v "režimu vícevláknového objektu apartment".</span><span class="sxs-lookup"><span data-stu-id="1c2de-127">-mta starts the ISE in “multi-threaded apartment mode”.</span></span> <span data-ttu-id="1c2de-128">Výchozí hodnota je s jedním vláknem.</span><span class="sxs-lookup"><span data-stu-id="1c2de-128">The default is single-threaded.</span></span>

<span data-ttu-id="1c2de-129">**Nové funkce editoru** bylo snazší vytvářet a číst váš kód:</span><span class="sxs-lookup"><span data-stu-id="1c2de-129">**New editor features** make it easier to create and read your code:</span></span>

- <span data-ttu-id="1c2de-130">**Barevné zvýrazňování syntaxe XML**.</span><span class="sxs-lookup"><span data-stu-id="1c2de-130">**XML syntax coloring**.</span></span> <span data-ttu-id="1c2de-131">Syntaxe jazyka XML ISE editor teď barvy stejným způsobem, jak barvy syntaxe kódu v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c2de-131">The ISE editor now colors XML syntax in the same way as it colors Windows PowerShell code syntax.</span></span>

- <span data-ttu-id="1c2de-132">**Párování závorek**.</span><span class="sxs-lookup"><span data-stu-id="1c2de-132">**Brace matching**.</span></span> <span data-ttu-id="1c2de-133">Prostředí PowerShell ISE ISEWindows zvýrazní odpovídající složené závorky vám pomohou zajistit máte správný počet pravé složené závorky tak, aby odpovídaly úvodním těch, které jsou.</span><span class="sxs-lookup"><span data-stu-id="1c2de-133">The ISEWindows PowerShell ISE highlights matching braces to help you ensure you have the right number of closing braces to match your opening ones.</span></span> <span data-ttu-id="1c2de-134">Pomocí CTRL -\[ najít odpovídající levou složenou závorku, které se kurzor nachází na pravé složené závorce.</span><span class="sxs-lookup"><span data-stu-id="1c2de-134">Use CTRL-\[ to locate the closing brace that matches the opening brace that the cursor is on.</span></span>

- <span data-ttu-id="1c2de-135">**Zobrazení osnovy**.</span><span class="sxs-lookup"><span data-stu-id="1c2de-135">**Outline view**.</span></span> <span data-ttu-id="1c2de-136">Můžete sbalit nebo rozbalit oddíly kódu kliknutím na tlačítko plus a minus na levém okraji.</span><span class="sxs-lookup"><span data-stu-id="1c2de-136">You can collapse or expand sections of your code by clicking the plus and minus signs in the left margin.</span></span> <span data-ttu-id="1c2de-137">Díky tomu je snazší najít kód, který hledáte dlouhé skriptu.</span><span class="sxs-lookup"><span data-stu-id="1c2de-137">This makes it easier to find the code you’re looking for in a long script.</span></span>

- <span data-ttu-id="1c2de-138">**Přetáhnout myší úpravy textu**.</span><span class="sxs-lookup"><span data-stu-id="1c2de-138">**Drag and drop text editing**.</span></span> <span data-ttu-id="1c2de-139">Můžete vybrat blok textu a přetáhněte ji do jiného umístění ji přesunout.</span><span class="sxs-lookup"><span data-stu-id="1c2de-139">You can select a block of text and drag it to another location to move it.</span></span> <span data-ttu-id="1c2de-140">Pokud podržíte stisknutou klávesu Ctrl při přetahování vybraný text, který je zkopírovat místo přesuňte.</span><span class="sxs-lookup"><span data-stu-id="1c2de-140">If you hold down the Ctrl key while you drag the selected text you copy instead of move.</span></span>

- <span data-ttu-id="1c2de-141">**Analýza chybových**.</span><span class="sxs-lookup"><span data-stu-id="1c2de-141">**Parse error display**.</span></span> <span data-ttu-id="1c2de-142">Prostředí Windows PowerShell prozkoumá váš skript při psaní.</span><span class="sxs-lookup"><span data-stu-id="1c2de-142">Windows PowerShell examines your script as you type.</span></span> <span data-ttu-id="1c2de-143">Pokud zjistí chybu, zobrazí červená vlnovka pod problematický kód.</span><span class="sxs-lookup"><span data-stu-id="1c2de-143">If it detects an error, it shows a red squiggle under the offending code.</span></span> <span data-ttu-id="1c2de-144">Když najedete myší uvedené chyby, popisek se dozvíte, problému, který nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="1c2de-144">When you hover over the indicated error, a tooltip shows you the problem that was found.</span></span>

- <span data-ttu-id="1c2de-145">**Přiblížení**.</span><span class="sxs-lookup"><span data-stu-id="1c2de-145">**Zoom**.</span></span> <span data-ttu-id="1c2de-146">Můžete přiblížit na vaše textu, aby bylo snazší pro čtení nebo oddálit, a prohlížení ve velkém s využitím posuvník v pravém dolním rohu okno integrovaného skriptovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="1c2de-146">You can zoom in on your text to make it easier to read or zoom out to see the bigger picture by using the slider in the bottom-right corner of the ISE window.</span></span>

- <span data-ttu-id="1c2de-147">**Formátovaný text zkopírovat a vložit**.</span><span class="sxs-lookup"><span data-stu-id="1c2de-147">**Rich text copy and paste**.</span></span> <span data-ttu-id="1c2de-148">Při kopírování z ISE do schránky, písmo, velikost a informace o barvě vybraného textu je v ceně.</span><span class="sxs-lookup"><span data-stu-id="1c2de-148">When you copy from the ISE to the clipboard, the font, size, and color information of the selected text is included.</span></span>

- <span data-ttu-id="1c2de-149">**Běr bloku**.</span><span class="sxs-lookup"><span data-stu-id="1c2de-149">**Block selection**.</span></span> <span data-ttu-id="1c2de-150">Můžete vybrat blok textu ve tvaru bloku tím, že podržíte stisknutou klávesu ALT při výběru text z podokna skriptu pomocí myši nebo stisknutím klávesy **Alt + Shift + šipka**.</span><span class="sxs-lookup"><span data-stu-id="1c2de-150">You can select a block-shaped chunk of text by holding down the ALT key while selecting text in the script pane with your mouse, or by pressing **Alt+Shift+Arrow**.</span></span>

### <a name="added-in-powershell-20-windows-server-2008-r2-windows-7"></a><span data-ttu-id="1c2de-151">Přidáno v prostředí PowerShell 2.0 (Windows Server 2008 R2, Windows 7)</span><span class="sxs-lookup"><span data-stu-id="1c2de-151">Added in PowerShell 2.0 (Windows Server 2008 R2, Windows 7)</span></span>

<span data-ttu-id="1c2de-152">ISE byla zavedená s Powershellem v2.0.</span><span class="sxs-lookup"><span data-stu-id="1c2de-152">The ISE was introduced with PowerShell v2.0.</span></span>

## <a name="requirements-for-running-the-windows-powershell-ise"></a><span data-ttu-id="1c2de-153">Požadavky na spuštění Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="1c2de-153">Requirements for running the Windows PowerShell ISE</span></span>

<span data-ttu-id="1c2de-154">ISE je dostupná na libovolném počítači Windows, který můžete spustit prostředí Windows PowerShell verze 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="1c2de-154">The ISE is available on any Windows computer that can run Windows PowerShell v2.0 or later.</span></span> <span data-ttu-id="1c2de-155">Zahrnuje každá verze Windows a Windows Server na verzi prostředí Windows PowerShell ISE, ale můžete upgradovat na nejnovější verzi dostupnou instalací Windows Management Frameworku (WMF).</span><span class="sxs-lookup"><span data-stu-id="1c2de-155">Each version of Windows and Windows Server includes a version of Windows PowerShell and the ISE, but you can upgrade to the latest available by installing the Windows Management Framework (WMF).</span></span> <span data-ttu-id="1c2de-156">Zobrazit [WMF](/powershell/wmf) Další informace naleznete v dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="1c2de-156">See the [WMF](/powershell/wmf) documentation for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="1c2de-157">Protože Windows PowerShell ISE vyžaduje grafické uživatelské rozhraní, nelze ji spustit v jádra serveru systému Windows Server.</span><span class="sxs-lookup"><span data-stu-id="1c2de-157">Because Windows PowerShell ISE requires a graphical user interface, you can’t run it on the Server Core option of Windows Server.</span></span>

## <a name="see-also"></a><span data-ttu-id="1c2de-158">Viz taky</span><span class="sxs-lookup"><span data-stu-id="1c2de-158">See also</span></span>

[<span data-ttu-id="1c2de-159">Účel skriptovacího objektového modelu windows power shell ise</span><span class="sxs-lookup"><span data-stu-id="1c2de-159">Purpose of the windows power shell ise scripting object model</span></span>](../../core-powershell/ise/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)