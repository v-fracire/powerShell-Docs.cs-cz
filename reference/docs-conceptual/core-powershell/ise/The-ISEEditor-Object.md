---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEEditor
ms.openlocfilehash: 2d4c3d941035384c591ca57e809c0e3a9b852f5c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952609"
---
# <a name="the-iseeditor-object"></a><span data-ttu-id="6d1c8-103">Objekt ISEEditor</span><span class="sxs-lookup"><span data-stu-id="6d1c8-103">The ISEEditor Object</span></span>

<span data-ttu-id="6d1c8-104">**ISEEditor** objekt je instance třídy Microsoft.PowerShell.Host.ISE.ISEEditor.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-104">An **ISEEditor** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEEditor class.</span></span> <span data-ttu-id="6d1c8-105">V podokně konzole je **ISEEditor** objektu.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-105">The Console pane is an **ISEEditor** object.</span></span> <span data-ttu-id="6d1c8-106">Každý [ISEFile](The-ISEFile-Object.md) objektů má přidruženou **ISEEditor** objektu.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-106">Each [ISEFile](The-ISEFile-Object.md) object has an associated **ISEEditor** object.</span></span> <span data-ttu-id="6d1c8-107">V následujících částech jsou uvedené metody a vlastnosti **ISEEditor** objektu.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-107">The following sections list the methods and properties of an **ISEEditor** object.</span></span>

## <a name="methods"></a><span data-ttu-id="6d1c8-108">Metody</span><span class="sxs-lookup"><span data-stu-id="6d1c8-108">Methods</span></span>

### <a name="clear"></a><span data-ttu-id="6d1c8-109">Zrušte zaškrtnutí\(\)</span><span class="sxs-lookup"><span data-stu-id="6d1c8-109">Clear\(\)</span></span>

<span data-ttu-id="6d1c8-110">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="6d1c8-111">Vymaže text v editoru.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-111">Clears the text in the editor.</span></span>

```powershell
# Clears the text in the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Clear()
```

### <a name="ensurevisibleint-linenumber"></a><span data-ttu-id="6d1c8-112">EnsureVisible\(int lineNumber\)</span><span class="sxs-lookup"><span data-stu-id="6d1c8-112">EnsureVisible\(int lineNumber\)</span></span>

<span data-ttu-id="6d1c8-113">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-113">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="6d1c8-114">Posune editoru tak, aby řádek, který odpovídá zadané **lineNumber** hodnota parametru je viditelná.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-114">Scrolls the editor so that the line that corresponds to the specified **lineNumber** parameter value is visible.</span></span> <span data-ttu-id="6d1c8-115">Ho vyvolá výjimku, pokud zadané číslo řádku je mimo rozsah 1, poslední číslo řádku, který definuje čísla platné řádků.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-115">It throws an exception if the specified line number is outside the range of 1,last line number, which defines the valid line numbers.</span></span>

<span data-ttu-id="6d1c8-116">**lineNumber** číslo řádku, který má být dostupná.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-116">**lineNumber** The number of the line that is to be made visible.</span></span>

```powershell
# Scrolls the text in the Script pane so that the fifth line is in view.
$psISE.CurrentFile.Editor.EnsureVisible(5)
```

### <a name="focus"></a><span data-ttu-id="6d1c8-117">Fokus\(\)</span><span class="sxs-lookup"><span data-stu-id="6d1c8-117">Focus\(\)</span></span>

<span data-ttu-id="6d1c8-118">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="6d1c8-119">Nastaví fokus na editoru.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-119">Sets the focus to the editor.</span></span>

```powershell
# Sets focus to the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### <a name="getlinelengthint-linenumber-"></a><span data-ttu-id="6d1c8-120">GetLineLength\(int lineNumber \)</span><span class="sxs-lookup"><span data-stu-id="6d1c8-120">GetLineLength\(int lineNumber \)</span></span>

<span data-ttu-id="6d1c8-121">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-121">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="6d1c8-122">Získá délku řádku jako celé číslo řádku, která je zadána číslo řádku.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-122">Gets the line length as an integer for the line that is specified by the line number.</span></span>

<span data-ttu-id="6d1c8-123">**lineNumber** číslo řádku, která se získat délku.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-123">**lineNumber** The number of the line of which to get the length.</span></span>

<span data-ttu-id="6d1c8-124">**Vrátí** délka řádku pro řádek na číslo zadané.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-124">**Returns** The line length for the line at the specified line number.</span></span>

```powershell
# Gets the length of the first line in the text of the Command pane.
$psISE.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### <a name="gotomatch"></a><span data-ttu-id="6d1c8-125">GoToMatch\(\)</span><span class="sxs-lookup"><span data-stu-id="6d1c8-125">GoToMatch\(\)</span></span>

<span data-ttu-id="6d1c8-126">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-126">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="6d1c8-127">Přesune vsuvka odpovídající znaku, pokud **CanGoToMatch** vlastností objektu editor je **$true**, která nastane, když pomocí kurzoru se bezprostředně před levé závorky, závorka nebo složené závorce - \(,\[, {- nebo ihned po uzavírací kulatá závorka, závorka nebo složené závorce - \),\],}.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-127">Moves the caret to the matching character if the **CanGoToMatch** property of the editor object is **$true**, which occurs when the caret is immediately before an opening parenthesis, bracket, or brace - \(,\[,{ - or immediately after a closing parenthesis, bracket, or brace - \),\],}.</span></span>  <span data-ttu-id="6d1c8-128">Pomocí kurzoru je umístěna před znakem otevírání nebo po ukončovací znak.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-128">The caret is placed before an opening character or after a closing character.</span></span> <span data-ttu-id="6d1c8-129">Pokud **CanGoToMatch** vlastnost je **$false**, pak tato metoda se nic nestane.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-129">If the **CanGoToMatch** property is **$false**, then this method does nothing.</span></span>

```powershell
# Goes to the matching character if CanGoToMatch() is $true
$psISE.CurrentPowerShellTab.ConsolePane.GoToMatch()
```

### <a name="inserttext-text-"></a><span data-ttu-id="6d1c8-130">InsertText\( textu \)</span><span class="sxs-lookup"><span data-stu-id="6d1c8-130">InsertText\( text \)</span></span>

<span data-ttu-id="6d1c8-131">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-131">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="6d1c8-132">Nahradí text výběr nebo vložení textu na aktuální pozici pomocí kurzoru.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-132">Replaces the selection with text or inserts text at the current caret position.</span></span>

<span data-ttu-id="6d1c8-133">**text** -řetězec text, který chcete vložit.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-133">**text** - String The text to insert.</span></span>

<span data-ttu-id="6d1c8-134">Najdete v článku [skriptování příklad](#scripting-example) dál v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-134">See the [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="select-startline-startcolumn-endline-endcolumn-"></a><span data-ttu-id="6d1c8-135">Vyberte\( startLine, Hodnota startColumn, ukončovacího endColumn \)</span><span class="sxs-lookup"><span data-stu-id="6d1c8-135">Select\( startLine, startColumn, endLine, endColumn \)</span></span>

<span data-ttu-id="6d1c8-136">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="6d1c8-137">Vybere text z **startLine**, **Hodnota startColumn**, **ukončovacího**, a **endColumn** parametry.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-137">Selects the text from the **startLine**, **startColumn**, **endLine**, and **endColumn** parameters.</span></span>

<span data-ttu-id="6d1c8-138">**startLine** -celé číslo řádku, kde začíná výběr.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-138">**startLine** - Integer The line where the selection starts.</span></span>

<span data-ttu-id="6d1c8-139">**Hodnota startColumn** -celé číslo sloupce v řádku počáteční kde výběr spustí.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-139">**startColumn** - Integer The column within the start line where the selection starts.</span></span>

<span data-ttu-id="6d1c8-140">**ukončovacího** -celé číslo řádku, které končí výběr.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-140">**endLine** - Integer The line where the selection ends.</span></span>

<span data-ttu-id="6d1c8-141">**endColumn** -celé číslo sloupce v rámci na konci řádku, které končí výběr.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-141">**endColumn** - Integer The column within the end line where the selection ends.</span></span>

<span data-ttu-id="6d1c8-142">Najdete v článku [skriptování příklad](#scripting-example) dál v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-142">See the  [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="selectcaretline"></a><span data-ttu-id="6d1c8-143">SelectCaretLine\(\)</span><span class="sxs-lookup"><span data-stu-id="6d1c8-143">SelectCaretLine\(\)</span></span>

<span data-ttu-id="6d1c8-144">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-144">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="6d1c8-145">Vybere celý řádek text, který aktuálně obsahuje pomocí kurzoru.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-145">Selects the entire line of text that currently contains the caret.</span></span>

```powershell
# First, set the caret position on line 5.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
# Now select that entire line of text
$psISE.CurrentFile.Editor.SelectCaretLine()
```

### <a name="setcaretposition-linenumber-columnnumber-"></a><span data-ttu-id="6d1c8-146">SetCaretPosition\( lineNumber čísla sloupce \)</span><span class="sxs-lookup"><span data-stu-id="6d1c8-146">SetCaretPosition\( lineNumber, columnNumber \)</span></span>

<span data-ttu-id="6d1c8-147">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-147">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="6d1c8-148">Nastavuje pozici pomocí kurzoru na řádku číslo a číslo sloupce.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-148">Sets the caret position at the line number and the column number.</span></span> <span data-ttu-id="6d1c8-149">Ho vyvolá výjimku, pokud pomocí kurzoru číslo řádku nebo pomocí kurzoru číslo sloupce je mimo jejich příslušné platné rozsahy.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-149">It throws an exception if either the caret line number  or the caret column number  are out of their respective valid ranges.</span></span>

<span data-ttu-id="6d1c8-150">**lineNumber** -celé číslo, číslo řádku pomocí kurzoru.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-150">**lineNumber** - Integer The caret line number.</span></span>

<span data-ttu-id="6d1c8-151">**čísla sloupce** -celé číslo číslo sloupce pomocí kurzoru.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-151">**columnNumber** - Integer The caret column number.</span></span>

```powershell
# Set the CaretPosition.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
```

### <a name="toggleoutliningexpansion"></a><span data-ttu-id="6d1c8-152">ToggleOutliningExpansion\(\)</span><span class="sxs-lookup"><span data-stu-id="6d1c8-152">ToggleOutliningExpansion\(\)</span></span>

<span data-ttu-id="6d1c8-153">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-153">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="6d1c8-154">Způsobí, že všechny části outline rozbalit nebo sbalit.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-154">Causes all the outline sections to expand or collapse.</span></span>

```powershell
# Toggle the outlining expansion
$psISE.CurrentFile.Editor.ToggleOutliningExpansion()
```

## <a name="properties"></a><span data-ttu-id="6d1c8-155">Properties</span><span class="sxs-lookup"><span data-stu-id="6d1c8-155">Properties</span></span>

### <a name="cangotomatch"></a><span data-ttu-id="6d1c8-156">CanGoToMatch</span><span class="sxs-lookup"><span data-stu-id="6d1c8-156">CanGoToMatch</span></span>

<span data-ttu-id="6d1c8-157">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-157">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="6d1c8-158">Jen pro čtení vlastnost typu Boolean označující, zda pomocí kurzoru vedle závorky, závorka nebo složené závorce - \( \), \[ \], {}.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-158">The read-only Boolean property to indicate whether the caret is next to a parenthesis, bracket, or brace - \(\), \[\], {}.</span></span> <span data-ttu-id="6d1c8-159">Pokud pomocí kurzoru se bezprostředně před znak otevírání nebo bezprostředně po ukončovací znak pár, pak je tato hodnota vlastnosti **$true**.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-159">If the caret is immediately before the opening character or immediately after the closing character of a pair, then this property value is **$true**.</span></span> <span data-ttu-id="6d1c8-160">Jinak je **$false**.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-160">Otherwise, it is **$false**.</span></span>

```powershell
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psISE.CurrentFile.Editor.CanGoToMatch
```

### <a name="caretcolumn"></a><span data-ttu-id="6d1c8-161">CaretColumn</span><span class="sxs-lookup"><span data-stu-id="6d1c8-161">CaretColumn</span></span>

<span data-ttu-id="6d1c8-162">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-162">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="6d1c8-163">Vlastnost jen pro čtení, který získá číslo sloupce, který odpovídá pozici pomocí kurzoru.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-163">The read-only property that gets the column number that corresponds to the position of the caret.</span></span>

```powershell
# Get the CaretColumn.
$psISE.CurrentFile.Editor.CaretColumn
```

### <a name="caretline"></a><span data-ttu-id="6d1c8-164">CaretLine</span><span class="sxs-lookup"><span data-stu-id="6d1c8-164">CaretLine</span></span>

<span data-ttu-id="6d1c8-165">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-165">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="6d1c8-166">Vlastnost jen pro čtení, který získá číslo řádku, který obsahuje pomocí kurzoru.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-166">The read-only property that gets the number of the line that contains the caret.</span></span>

```powershell
# Get the CaretLine.
$psISE.CurrentFile.Editor.CaretLine
```

### <a name="caretlinetext"></a><span data-ttu-id="6d1c8-167">CaretLineText</span><span class="sxs-lookup"><span data-stu-id="6d1c8-167">CaretLineText</span></span>

<span data-ttu-id="6d1c8-168">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-168">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="6d1c8-169">Vlastnost jen pro čtení, který získá úplný řádek textu, který obsahuje pomocí kurzoru.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-169">The read-only property that gets the complete line of text that contains the caret.</span></span>

```powershell
# Get all of the text on the line that contains the caret.
$psISE.CurrentFile.Editor.CaretLineText
```

### <a name="linecount"></a><span data-ttu-id="6d1c8-170">LineCount</span><span class="sxs-lookup"><span data-stu-id="6d1c8-170">LineCount</span></span>

<span data-ttu-id="6d1c8-171">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-171">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="6d1c8-172">Vlastnost jen pro čtení, získá počet řádků v editoru.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-172">The read-only property that gets the line count from the editor.</span></span>

```powershell
# Get the LineCount.
$psISE.CurrentFile.Editor.LineCount
```

### <a name="selectedtext"></a><span data-ttu-id="6d1c8-173">SelectedText</span><span class="sxs-lookup"><span data-stu-id="6d1c8-173">SelectedText</span></span>

<span data-ttu-id="6d1c8-174">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-174">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="6d1c8-175">Vlastnost jen pro čtení, získá vybraný text v editoru.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-175">The read-only property that gets the selected text from the editor.</span></span>

<span data-ttu-id="6d1c8-176">Najdete v článku [skriptování příklad](#scripting-example) dál v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-176">See the  [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="text"></a><span data-ttu-id="6d1c8-177">Text</span><span class="sxs-lookup"><span data-stu-id="6d1c8-177">Text</span></span>

<span data-ttu-id="6d1c8-178">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-178">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="6d1c8-179">Vlastnost pro čtení a zápis, který získá nebo nastaví text v editoru.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-179">The read/write property that gets or sets the text in the editor.</span></span>

<span data-ttu-id="6d1c8-180">Najdete v článku [skriptování příklad](#scripting-example) dál v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="6d1c8-180">See the [Scripting Example](#scripting-example) later in this topic.</span></span>

## <a name="scripting-example"></a><span data-ttu-id="6d1c8-181">Příklad skriptování</span><span class="sxs-lookup"><span data-stu-id="6d1c8-181">Scripting Example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="6d1c8-182">Viz také</span><span class="sxs-lookup"><span data-stu-id="6d1c8-182">See Also</span></span>

- [<span data-ttu-id="6d1c8-183">Objekt ISEFile</span><span class="sxs-lookup"><span data-stu-id="6d1c8-183">The ISEFile Object</span></span>](The-ISEFile-Object.md)
- [<span data-ttu-id="6d1c8-184">Objekt PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="6d1c8-184">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="6d1c8-185">Účelem ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="6d1c8-185">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="6d1c8-186">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="6d1c8-186">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)