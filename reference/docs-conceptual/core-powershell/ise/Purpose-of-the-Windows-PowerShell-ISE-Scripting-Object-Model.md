---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Účelem ISE Windows PowerShell skriptování objektový Model"
ms.assetid: d176a131-ab0c-43ee-80c1-f824ab8e4a05
ms.openlocfilehash: 3256d8bff3885d266f0db6f52932e40c4beaf8b1
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="purpose-of-the-windows-powershell-ise-scripting-object-model"></a><span data-ttu-id="97122-103">Účelem ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="97122-103">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>
  <span data-ttu-id="97122-104">Objekty jsou přidružené k formuláře a funkce systému Windows PowerShell Integrované skriptovací prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="97122-104">Objects are associated with the form and function of Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="97122-105">Odkaz na objekt modelu poskytuje podrobnosti o člen vlastnosti a metody, které zveřejňují tyto objekty.</span><span class="sxs-lookup"><span data-stu-id="97122-105">The object model reference provides details about the member properties and methods that these objects expose.</span></span> <span data-ttu-id="97122-106">Příklady slouží k zobrazení, jak můžete použít skripty přímý přístup k tyto metody a vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="97122-106">Examples are provided to show how you can use scripts to directly access these methods and properties.</span></span> <span data-ttu-id="97122-107">Skriptovací objektový model usnadňuje následující řadu úloh.</span><span class="sxs-lookup"><span data-stu-id="97122-107">The scripting object model makes the following range of tasks easier.</span></span>

## <a name="customizing-the-appearance-of-windows-powershell-ise"></a><span data-ttu-id="97122-108">Přizpůsobení vzhledu Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="97122-108">Customizing the appearance of Windows PowerShell ISE</span></span>
 <span data-ttu-id="97122-109">Objektový model můžete upravit nastavení aplikace a možnosti.</span><span class="sxs-lookup"><span data-stu-id="97122-109">You can use the object model to modify the application settings and options.</span></span> <span data-ttu-id="97122-110">Například můžete je upravit takto:</span><span class="sxs-lookup"><span data-stu-id="97122-110">For example, you can modify them as follows:</span></span>

- <span data-ttu-id="97122-111">Můžete změnit barvu chyby, upozornění, podrobné výstupy a ladění výstupu.</span><span class="sxs-lookup"><span data-stu-id="97122-111">You can change the color of errors, warnings, verbose outputs, and debug outputs.</span></span>

- <span data-ttu-id="97122-112">Můžete získat nebo nastavit barvy pozadí v podokně příkaz, podokno výstup a v podokně skriptu.</span><span class="sxs-lookup"><span data-stu-id="97122-112">You can get or set the background colors for the Command pane, the Output pane, and the Script pane.</span></span>

- <span data-ttu-id="97122-113">Můžete nastavit barvu popředí podokno výstup.</span><span class="sxs-lookup"><span data-stu-id="97122-113">You can set the foreground color for the Output pane.</span></span>

- <span data-ttu-id="97122-114">Název písma a velikost písma lze nastavit pro Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="97122-114">You can set the font name and font size for Windows PowerShell ISE.</span></span>

- <span data-ttu-id="97122-115">Můžete konfigurovat upozornění.</span><span class="sxs-lookup"><span data-stu-id="97122-115">You can configure warnings.</span></span> <span data-ttu-id="97122-116">Toto nastavení zahrnuje upozornění, které jsou vydány po otevření souboru v několik karet prostředí PowerShell nebo pokud se předtím, než byl uložen soubor, spustí se skript v souboru.</span><span class="sxs-lookup"><span data-stu-id="97122-116">This setting includes warnings that are issued when a file is opened in multiple PowerShell tabs or when a script in the file is run before the file has been saved.</span></span>

- <span data-ttu-id="97122-117">Můžete přepínat mezi zobrazení, kdy jsou v podokně skriptu a v podokně výstup vedle sebe a zobrazení kde v podokně skriptu je nad podokno výstup.</span><span class="sxs-lookup"><span data-stu-id="97122-117">You can switch between a view where the Script pane and the Output pane are side-by-side and a view where the Script pane is on top of the Output pane.</span></span> <span data-ttu-id="97122-118">V podokně příkaz můžete ukotvit dolní nebo horní podokno výstup.</span><span class="sxs-lookup"><span data-stu-id="97122-118">You can dock the Command pane to the bottom or the top of the Output pane.</span></span>

## <a name="enhancing-the-functionality-of-windows-powershell-ise"></a><span data-ttu-id="97122-119">Rozšíření funkce systému Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="97122-119">Enhancing the functionality of Windows PowerShell ISE</span></span>
 <span data-ttu-id="97122-120">Objektový model můžete použít k rozšíření funkcí Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="97122-120">You can use the object model to enhance the functionality of Windows PowerShell ISE.</span></span> <span data-ttu-id="97122-121">Například můžete:</span><span class="sxs-lookup"><span data-stu-id="97122-121">For example, you can:</span></span>

- <span data-ttu-id="97122-122">Přidání a změna instanci ISE Windows PowerShell, sám sebe.</span><span class="sxs-lookup"><span data-stu-id="97122-122">Add and modify the instance of Windows PowerShell ISE itself.</span></span> <span data-ttu-id="97122-123">Chcete-li změnit v nabídkách, můžete například přidávat nové položky nabídky a nové položky nabídky mapy skriptů.</span><span class="sxs-lookup"><span data-stu-id="97122-123">For example, to change the menus, you can add new menu items and map the new menu items to scripts.</span></span>

- <span data-ttu-id="97122-124">Vytvořte skripty, které provést některé úlohy, které můžete provádět pomocí tlačítka a příkazy nabídky v systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="97122-124">Create scripts that perform some of the tasks that you can perform by using the menu commands and buttons in Windows PowerShell ISE.</span></span> <span data-ttu-id="97122-125">Například můžete přidat, odebrat nebo vyberte na kartě prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97122-125">For example, you can add, remove, or select a PowerShell tab.</span></span>

- <span data-ttu-id="97122-126">Doplňkovým úlohy, které lze provést pomocí tlačítka a příkazy nabídky.</span><span class="sxs-lookup"><span data-stu-id="97122-126">Complement tasks that can be performed by using menu commands and buttons.</span></span> <span data-ttu-id="97122-127">Můžete například přejmenovat na kartě prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97122-127">For example, you can rename a PowerShell tab.</span></span>

- <span data-ttu-id="97122-128">Upravit textové vyrovnávací paměti pro příkaz podokno, podokno výstup a v podokně skriptu, přidružené k souboru.</span><span class="sxs-lookup"><span data-stu-id="97122-128">Manipulate text buffers for the Command pane, the Output pane, and the Script pane that are associated with a file.</span></span> <span data-ttu-id="97122-129">Například můžete:</span><span class="sxs-lookup"><span data-stu-id="97122-129">For example, you can:</span></span>

    -   <span data-ttu-id="97122-130">Získání nebo nastavení veškerého textu.</span><span class="sxs-lookup"><span data-stu-id="97122-130">Get or set all text.</span></span>

    -   <span data-ttu-id="97122-131">Získání nebo nastavení výběr textu.</span><span class="sxs-lookup"><span data-stu-id="97122-131">Get or set a text selection.</span></span>

    -   <span data-ttu-id="97122-132">Spuštění skriptu nebo spustit vybranou část skriptu.</span><span class="sxs-lookup"><span data-stu-id="97122-132">Run a script or run a selected portion of a script.</span></span>

    -   <span data-ttu-id="97122-133">Na řádku přejděte do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="97122-133">Scroll a line into view.</span></span>

    -   <span data-ttu-id="97122-134">Vložte text na pozici pomocí kurzoru.</span><span class="sxs-lookup"><span data-stu-id="97122-134">Insert text at a caret position.</span></span>

    -   <span data-ttu-id="97122-135">Vyberte blok textu.</span><span class="sxs-lookup"><span data-stu-id="97122-135">Select a block of text.</span></span>

    -   <span data-ttu-id="97122-136">Získejte poslední číslo řádku.</span><span class="sxs-lookup"><span data-stu-id="97122-136">Get the last line number.</span></span>

- <span data-ttu-id="97122-137">Provedení operace se soubory.</span><span class="sxs-lookup"><span data-stu-id="97122-137">Perform file operations.</span></span> <span data-ttu-id="97122-138">Například můžete:</span><span class="sxs-lookup"><span data-stu-id="97122-138">For example, you can:</span></span>

    -   <span data-ttu-id="97122-139">Otevření souboru, uložit soubor nebo uložení souboru pomocí jiný název.</span><span class="sxs-lookup"><span data-stu-id="97122-139">Open a file, save a file, or save a file by using a different name.</span></span>

    -   <span data-ttu-id="97122-140">Určí, zda soubor byla změněna od posledního uložení.</span><span class="sxs-lookup"><span data-stu-id="97122-140">Determine whether a file has been changed after it was last saved.</span></span>

    -   <span data-ttu-id="97122-141">Získání názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="97122-141">Get the file name.</span></span>

    -   <span data-ttu-id="97122-142">Vyberte soubor.</span><span class="sxs-lookup"><span data-stu-id="97122-142">Select a file.</span></span>

## <a name="automating-tasks"></a><span data-ttu-id="97122-143">Automatizaci úloh</span><span class="sxs-lookup"><span data-stu-id="97122-143">Automating tasks</span></span>
 <span data-ttu-id="97122-144">Skriptovací objekt modelu můžete použít k vytvoření klávesové zkratky pro časté operace.</span><span class="sxs-lookup"><span data-stu-id="97122-144">You can use the scripting object model to create keyboard shortcuts for frequent operations.</span></span>

## <a name="see-also"></a><span data-ttu-id="97122-145">Viz také</span><span class="sxs-lookup"><span data-stu-id="97122-145">See Also</span></span>
- [<span data-ttu-id="97122-146">Hierarchie ISE objektů modelu</span><span class="sxs-lookup"><span data-stu-id="97122-146">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md) 
- [<span data-ttu-id="97122-147">Odkaz na objekt modelu Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="97122-147">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="97122-148">ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="97122-148">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)

  
