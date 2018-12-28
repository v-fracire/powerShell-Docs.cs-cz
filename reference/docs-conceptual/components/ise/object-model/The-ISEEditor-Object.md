---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEEditor
ms.openlocfilehash: 2d4c3d941035384c591ca57e809c0e3a9b852f5c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404063"
---
# <a name="the-iseeditor-object"></a><span data-ttu-id="646ec-103">Objekt ISEEditor</span><span class="sxs-lookup"><span data-stu-id="646ec-103">The ISEEditor Object</span></span>

<span data-ttu-id="646ec-104">**ISEEditor** je objekt instancí třídy Microsoft.PowerShell.Host.ISE.ISEEditor.</span><span class="sxs-lookup"><span data-stu-id="646ec-104">An **ISEEditor** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEEditor class.</span></span> <span data-ttu-id="646ec-105">V podokně konzoly je **ISEEditor** objektu.</span><span class="sxs-lookup"><span data-stu-id="646ec-105">The Console pane is an **ISEEditor** object.</span></span> <span data-ttu-id="646ec-106">Každý [ISEFile](The-ISEFile-Object.md) objektů má přidruženou **ISEEditor** objektu.</span><span class="sxs-lookup"><span data-stu-id="646ec-106">Each [ISEFile](The-ISEFile-Object.md) object has an associated **ISEEditor** object.</span></span> <span data-ttu-id="646ec-107">V následujících oddílech jsou uvedeny metody a vlastnosti **ISEEditor** objektu.</span><span class="sxs-lookup"><span data-stu-id="646ec-107">The following sections list the methods and properties of an **ISEEditor** object.</span></span>

## <a name="methods"></a><span data-ttu-id="646ec-108">Metody</span><span class="sxs-lookup"><span data-stu-id="646ec-108">Methods</span></span>

### <a name="clear"></a><span data-ttu-id="646ec-109">Vymazat\(\)</span><span class="sxs-lookup"><span data-stu-id="646ec-109">Clear\(\)</span></span>

<span data-ttu-id="646ec-110">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="646ec-111">Vymaže textu v editoru.</span><span class="sxs-lookup"><span data-stu-id="646ec-111">Clears the text in the editor.</span></span>

```powershell
# Clears the text in the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Clear()
```

### <a name="ensurevisibleint-linenumber"></a><span data-ttu-id="646ec-112">EnsureVisible\(int lineNumber\)</span><span class="sxs-lookup"><span data-stu-id="646ec-112">EnsureVisible\(int lineNumber\)</span></span>

<span data-ttu-id="646ec-113">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-113">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="646ec-114">Posune editor tak, aby řádek, který odpovídá zadané **lineNumber** hodnota parametru je viditelný.</span><span class="sxs-lookup"><span data-stu-id="646ec-114">Scrolls the editor so that the line that corresponds to the specified **lineNumber** parameter value is visible.</span></span> <span data-ttu-id="646ec-115">Vyvolá výjimku, pokud zadaný počet řádků je mimo rozsah 1, poslední číslo řádku, který definuje platné ků.</span><span class="sxs-lookup"><span data-stu-id="646ec-115">It throws an exception if the specified line number is outside the range of 1,last line number, which defines the valid line numbers.</span></span>

<span data-ttu-id="646ec-116">**Číslo řádku** číslo řádku, který má být nastavena jako viditelná.</span><span class="sxs-lookup"><span data-stu-id="646ec-116">**lineNumber** The number of the line that is to be made visible.</span></span>

```powershell
# Scrolls the text in the Script pane so that the fifth line is in view.
$psISE.CurrentFile.Editor.EnsureVisible(5)
```

### <a name="focus"></a><span data-ttu-id="646ec-117">Fokus\(\)</span><span class="sxs-lookup"><span data-stu-id="646ec-117">Focus\(\)</span></span>

<span data-ttu-id="646ec-118">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="646ec-119">Nastaví zaměření na editor.</span><span class="sxs-lookup"><span data-stu-id="646ec-119">Sets the focus to the editor.</span></span>

```powershell
# Sets focus to the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### <a name="getlinelengthint-linenumber-"></a><span data-ttu-id="646ec-120">GetLineLength\(int lineNumber \)</span><span class="sxs-lookup"><span data-stu-id="646ec-120">GetLineLength\(int lineNumber \)</span></span>

<span data-ttu-id="646ec-121">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-121">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="646ec-122">Získá délku řádku jako celé číslo řádku, který je určený číslem řádku.</span><span class="sxs-lookup"><span data-stu-id="646ec-122">Gets the line length as an integer for the line that is specified by the line number.</span></span>

<span data-ttu-id="646ec-123">**Číslo řádku** číslo řádku, ze kterého se má získat délka.</span><span class="sxs-lookup"><span data-stu-id="646ec-123">**lineNumber** The number of the line of which to get the length.</span></span>

<span data-ttu-id="646ec-124">**Vrátí** délka řádku pro řádek na zadaný počet řádků.</span><span class="sxs-lookup"><span data-stu-id="646ec-124">**Returns** The line length for the line at the specified line number.</span></span>

```powershell
# Gets the length of the first line in the text of the Command pane.
$psISE.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### <a name="gotomatch"></a><span data-ttu-id="646ec-125">GoToMatch\(\)</span><span class="sxs-lookup"><span data-stu-id="646ec-125">GoToMatch\(\)</span></span>

<span data-ttu-id="646ec-126">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-126">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="646ec-127">Přesune blikající kurzor na odpovídající znak, pokud **CanGoToMatch** vlastností objektu editoru je **$true**, která nastane, pokud kurzor se bezprostředně před levou závorku, závorky nebo složenou závorku - \(,\[, {- nebo ihned za pravou závorku, závorky nebo složenou závorku - \),\],}.</span><span class="sxs-lookup"><span data-stu-id="646ec-127">Moves the caret to the matching character if the **CanGoToMatch** property of the editor object is **$true**, which occurs when the caret is immediately before an opening parenthesis, bracket, or brace - \(,\[,{ - or immediately after a closing parenthesis, bracket, or brace - \),\],}.</span></span>  <span data-ttu-id="646ec-128">Blikající kurzor je umístěn před počáteční znak nebo po ukončovací znak.</span><span class="sxs-lookup"><span data-stu-id="646ec-128">The caret is placed before an opening character or after a closing character.</span></span> <span data-ttu-id="646ec-129">Pokud **CanGoToMatch** vlastnost **$false**, pak tato metoda nemá žádný účinek.</span><span class="sxs-lookup"><span data-stu-id="646ec-129">If the **CanGoToMatch** property is **$false**, then this method does nothing.</span></span>

```powershell
# Goes to the matching character if CanGoToMatch() is $true
$psISE.CurrentPowerShellTab.ConsolePane.GoToMatch()
```

### <a name="inserttext-text-"></a><span data-ttu-id="646ec-130">InsertText\( text \)</span><span class="sxs-lookup"><span data-stu-id="646ec-130">InsertText\( text \)</span></span>

<span data-ttu-id="646ec-131">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-131">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="646ec-132">Nahradí text výběru nebo vloží text na aktuální pozici blikajícího kurzoru.</span><span class="sxs-lookup"><span data-stu-id="646ec-132">Replaces the selection with text or inserts text at the current caret position.</span></span>

<span data-ttu-id="646ec-133">**text** – text, který chcete vložit řetězec.</span><span class="sxs-lookup"><span data-stu-id="646ec-133">**text** - String The text to insert.</span></span>

<span data-ttu-id="646ec-134">Zobrazit [skriptování příklad](#scripting-example) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="646ec-134">See the [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="select-startline-startcolumn-endline-endcolumn-"></a><span data-ttu-id="646ec-135">Vyberte\( startLine startColumn, ukončovacího endColumn \)</span><span class="sxs-lookup"><span data-stu-id="646ec-135">Select\( startLine, startColumn, endLine, endColumn \)</span></span>

<span data-ttu-id="646ec-136">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="646ec-137">Vybere text z **startLine**, **startColumn**, **ukončovacího**, a **endColumn** parametry.</span><span class="sxs-lookup"><span data-stu-id="646ec-137">Selects the text from the **startLine**, **startColumn**, **endLine**, and **endColumn** parameters.</span></span>

<span data-ttu-id="646ec-138">**startLine** – celé číslo řádku, kde začíná výběr.</span><span class="sxs-lookup"><span data-stu-id="646ec-138">**startLine** - Integer The line where the selection starts.</span></span>

<span data-ttu-id="646ec-139">**startColumn** – celé číslo sloupce v řádku start, kde začíná výběr.</span><span class="sxs-lookup"><span data-stu-id="646ec-139">**startColumn** - Integer The column within the start line where the selection starts.</span></span>

<span data-ttu-id="646ec-140">**ukončovacího** – celé číslo řádku, kde končí výběr.</span><span class="sxs-lookup"><span data-stu-id="646ec-140">**endLine** - Integer The line where the selection ends.</span></span>

<span data-ttu-id="646ec-141">**endColumn** – celé číslo sloupce v rámci na konci řádku, kde končí výběr.</span><span class="sxs-lookup"><span data-stu-id="646ec-141">**endColumn** - Integer The column within the end line where the selection ends.</span></span>

<span data-ttu-id="646ec-142">Zobrazit [skriptování příklad](#scripting-example) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="646ec-142">See the  [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="selectcaretline"></a><span data-ttu-id="646ec-143">SelectCaretLine\(\)</span><span class="sxs-lookup"><span data-stu-id="646ec-143">SelectCaretLine\(\)</span></span>

<span data-ttu-id="646ec-144">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-144">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="646ec-145">Vybere celý řádek textu, který je v současné době obsahuje blikajícího kurzoru.</span><span class="sxs-lookup"><span data-stu-id="646ec-145">Selects the entire line of text that currently contains the caret.</span></span>

```powershell
# First, set the caret position on line 5.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
# Now select that entire line of text
$psISE.CurrentFile.Editor.SelectCaretLine()
```

### <a name="setcaretposition-linenumber-columnnumber-"></a><span data-ttu-id="646ec-146">SetCaretPosition\( číslo řádku, columnNumber \)</span><span class="sxs-lookup"><span data-stu-id="646ec-146">SetCaretPosition\( lineNumber, columnNumber \)</span></span>

<span data-ttu-id="646ec-147">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-147">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="646ec-148">Nastaví pozici blikajícího kurzoru na řádku číslo a číslo sloupce.</span><span class="sxs-lookup"><span data-stu-id="646ec-148">Sets the caret position at the line number and the column number.</span></span> <span data-ttu-id="646ec-149">Vyvolá výjimku, pokud je číslo řádku stříška nebo číslo sloupce blikající kurzor nedodržují jejich odpovídajících platné rozsahy.</span><span class="sxs-lookup"><span data-stu-id="646ec-149">It throws an exception if either the caret line number  or the caret column number  are out of their respective valid ranges.</span></span>

<span data-ttu-id="646ec-150">**Číslo řádku** – celé číslo, číslo řádku blikajícího kurzoru.</span><span class="sxs-lookup"><span data-stu-id="646ec-150">**lineNumber** - Integer The caret line number.</span></span>

<span data-ttu-id="646ec-151">**columnNumber** – celé číslo číslo sloupce blikajícího kurzoru.</span><span class="sxs-lookup"><span data-stu-id="646ec-151">**columnNumber** - Integer The caret column number.</span></span>

```powershell
# Set the CaretPosition.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
```

### <a name="toggleoutliningexpansion"></a><span data-ttu-id="646ec-152">ToggleOutliningExpansion\(\)</span><span class="sxs-lookup"><span data-stu-id="646ec-152">ToggleOutliningExpansion\(\)</span></span>

<span data-ttu-id="646ec-153">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-153">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="646ec-154">Způsobí, že všechny části osnovy rozbalit nebo sbalit.</span><span class="sxs-lookup"><span data-stu-id="646ec-154">Causes all the outline sections to expand or collapse.</span></span>

```powershell
# Toggle the outlining expansion
$psISE.CurrentFile.Editor.ToggleOutliningExpansion()
```

## <a name="properties"></a><span data-ttu-id="646ec-155">Properties</span><span class="sxs-lookup"><span data-stu-id="646ec-155">Properties</span></span>

### <a name="cangotomatch"></a><span data-ttu-id="646ec-156">CanGoToMatch</span><span class="sxs-lookup"><span data-stu-id="646ec-156">CanGoToMatch</span></span>

<span data-ttu-id="646ec-157">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-157">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="646ec-158">Logická vlastnost jen pro čtení k určení, jestli je blikající kurzor vedle závorky, závorky nebo složenou závorku - \( \), \[ \], {}.</span><span class="sxs-lookup"><span data-stu-id="646ec-158">The read-only Boolean property to indicate whether the caret is next to a parenthesis, bracket, or brace - \(\), \[\], {}.</span></span> <span data-ttu-id="646ec-159">Pokud kurzor se bezprostředně před počáteční znak nebo bezprostředně po koncový znak z dvojice, pak je tato hodnota vlastnosti **$true**.</span><span class="sxs-lookup"><span data-stu-id="646ec-159">If the caret is immediately before the opening character or immediately after the closing character of a pair, then this property value is **$true**.</span></span> <span data-ttu-id="646ec-160">V opačném případě je **$false**.</span><span class="sxs-lookup"><span data-stu-id="646ec-160">Otherwise, it is **$false**.</span></span>

```powershell
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psISE.CurrentFile.Editor.CanGoToMatch
```

### <a name="caretcolumn"></a><span data-ttu-id="646ec-161">CaretColumn</span><span class="sxs-lookup"><span data-stu-id="646ec-161">CaretColumn</span></span>

<span data-ttu-id="646ec-162">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-162">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="646ec-163">Vlastnost jen pro čtení, který získá číslo sloupce, který odpovídá pozici blikajícího kurzoru.</span><span class="sxs-lookup"><span data-stu-id="646ec-163">The read-only property that gets the column number that corresponds to the position of the caret.</span></span>

```powershell
# Get the CaretColumn.
$psISE.CurrentFile.Editor.CaretColumn
```

### <a name="caretline"></a><span data-ttu-id="646ec-164">CaretLine</span><span class="sxs-lookup"><span data-stu-id="646ec-164">CaretLine</span></span>

<span data-ttu-id="646ec-165">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-165">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="646ec-166">Vlastnost jen pro čtení, která získá počet řádků, které obsahuje blikajícího kurzoru.</span><span class="sxs-lookup"><span data-stu-id="646ec-166">The read-only property that gets the number of the line that contains the caret.</span></span>

```powershell
# Get the CaretLine.
$psISE.CurrentFile.Editor.CaretLine
```

### <a name="caretlinetext"></a><span data-ttu-id="646ec-167">CaretLineText</span><span class="sxs-lookup"><span data-stu-id="646ec-167">CaretLineText</span></span>

<span data-ttu-id="646ec-168">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-168">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="646ec-169">Vlastnost jen pro čtení, která vrací úplný řádek text, který obsahuje blikajícího kurzoru.</span><span class="sxs-lookup"><span data-stu-id="646ec-169">The read-only property that gets the complete line of text that contains the caret.</span></span>

```powershell
# Get all of the text on the line that contains the caret.
$psISE.CurrentFile.Editor.CaretLineText
```

### <a name="linecount"></a><span data-ttu-id="646ec-170">LineCount</span><span class="sxs-lookup"><span data-stu-id="646ec-170">LineCount</span></span>

<span data-ttu-id="646ec-171">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-171">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="646ec-172">Vlastnost jen pro čtení, která získá počet řádků v editoru.</span><span class="sxs-lookup"><span data-stu-id="646ec-172">The read-only property that gets the line count from the editor.</span></span>

```powershell
# Get the LineCount.
$psISE.CurrentFile.Editor.LineCount
```

### <a name="selectedtext"></a><span data-ttu-id="646ec-173">SelectedText</span><span class="sxs-lookup"><span data-stu-id="646ec-173">SelectedText</span></span>

<span data-ttu-id="646ec-174">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-174">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="646ec-175">Vlastnost jen pro čtení, která získá vybraný text z editoru.</span><span class="sxs-lookup"><span data-stu-id="646ec-175">The read-only property that gets the selected text from the editor.</span></span>

<span data-ttu-id="646ec-176">Zobrazit [skriptování příklad](#scripting-example) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="646ec-176">See the  [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="text"></a><span data-ttu-id="646ec-177">Text</span><span class="sxs-lookup"><span data-stu-id="646ec-177">Text</span></span>

<span data-ttu-id="646ec-178">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="646ec-178">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="646ec-179">Vlastnost pro čtení a zápis, která získá nebo nastaví text v editoru.</span><span class="sxs-lookup"><span data-stu-id="646ec-179">The read/write property that gets or sets the text in the editor.</span></span>

<span data-ttu-id="646ec-180">Zobrazit [skriptování příklad](#scripting-example) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="646ec-180">See the [Scripting Example](#scripting-example) later in this topic.</span></span>

## <a name="scripting-example"></a><span data-ttu-id="646ec-181">Příklad skriptu</span><span class="sxs-lookup"><span data-stu-id="646ec-181">Scripting Example</span></span>

```powershell
# This illustrates how you can use the length of a line to
# select the entire line and shows how you can make it lowercase.
# You must run this in the Console pane. It will not run in the Script pane.
# Begin by getting a variable that points to the editor.
$myEditor = $psISE.CurrentFile.Editor
# Clear the text in the current file editor.
$myEditor.Clear()

# Make sure the file has five lines of text.
$myEditor.InsertText("LINE1 `n")
$myEditor.InsertText("LINE2 `n")
$myEditor.InsertText("LINE3 `n")
$myEditor.InsertText("LINE4 `n")
$myEditor.InsertText("LINE5 `n")

# Use the GetLineLength method to get the length of the third line.
$endColumn = $myEditor.GetLineLength(3)
# Select the text in the first three lines.
$myEditor.Select(1, 1, 3, $endColumn + 1)
$selection = $myEditor.SelectedText
# Clear all the text in the editor.
$myEditor.Clear()
# Add the selected text back, but in lower case.
$myEditor.InsertText($selection.ToLower())
```

## <a name="see-also"></a><span data-ttu-id="646ec-182">Viz také</span><span class="sxs-lookup"><span data-stu-id="646ec-182">See Also</span></span>

- [<span data-ttu-id="646ec-183">Objekt ISEFile</span><span class="sxs-lookup"><span data-stu-id="646ec-183">The ISEFile Object</span></span>](The-ISEFile-Object.md)
- [<span data-ttu-id="646ec-184">Objekt PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="646ec-184">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="646ec-185">Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="646ec-185">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="646ec-186">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="646ec-186">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)