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
# <a name="the-iseeditor-object"></a>Objekt ISEEditor

**ISEEditor** je objekt instancí třídy Microsoft.PowerShell.Host.ISE.ISEEditor. V podokně konzoly je **ISEEditor** objektu. Každý [ISEFile](The-ISEFile-Object.md) objektů má přidruženou **ISEEditor** objektu. V následujících oddílech jsou uvedeny metody a vlastnosti **ISEEditor** objektu.

## <a name="methods"></a>Metody

### <a name="clear"></a>Vymazat\(\)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vymaže textu v editoru.

```powershell
# Clears the text in the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Clear()
```

### <a name="ensurevisibleint-linenumber"></a>EnsureVisible\(int lineNumber\)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Posune editor tak, aby řádek, který odpovídá zadané **lineNumber** hodnota parametru je viditelný. Vyvolá výjimku, pokud zadaný počet řádků je mimo rozsah 1, poslední číslo řádku, který definuje platné ků.

**Číslo řádku** číslo řádku, který má být nastavena jako viditelná.

```powershell
# Scrolls the text in the Script pane so that the fifth line is in view.
$psISE.CurrentFile.Editor.EnsureVisible(5)
```

### <a name="focus"></a>Fokus\(\)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Nastaví zaměření na editor.

```powershell
# Sets focus to the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### <a name="getlinelengthint-linenumber-"></a>GetLineLength\(int lineNumber \)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Získá délku řádku jako celé číslo řádku, který je určený číslem řádku.

**Číslo řádku** číslo řádku, ze kterého se má získat délka.

**Vrátí** délka řádku pro řádek na zadaný počet řádků.

```powershell
# Gets the length of the first line in the text of the Command pane.
$psISE.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### <a name="gotomatch"></a>GoToMatch\(\)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Přesune blikající kurzor na odpovídající znak, pokud **CanGoToMatch** vlastností objektu editoru je **$true**, která nastane, pokud kurzor se bezprostředně před levou závorku, závorky nebo složenou závorku - \(,\[, {- nebo ihned za pravou závorku, závorky nebo složenou závorku - \),\],}.  Blikající kurzor je umístěn před počáteční znak nebo po ukončovací znak. Pokud **CanGoToMatch** vlastnost **$false**, pak tato metoda nemá žádný účinek.

```powershell
# Goes to the matching character if CanGoToMatch() is $true
$psISE.CurrentPowerShellTab.ConsolePane.GoToMatch()
```

### <a name="inserttext-text-"></a>InsertText\( text \)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Nahradí text výběru nebo vloží text na aktuální pozici blikajícího kurzoru.

**text** – text, který chcete vložit řetězec.

Zobrazit [skriptování příklad](#scripting-example) dále v tomto tématu.

### <a name="select-startline-startcolumn-endline-endcolumn-"></a>Vyberte\( startLine startColumn, ukončovacího endColumn \)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vybere text z **startLine**, **startColumn**, **ukončovacího**, a **endColumn** parametry.

**startLine** – celé číslo řádku, kde začíná výběr.

**startColumn** – celé číslo sloupce v řádku start, kde začíná výběr.

**ukončovacího** – celé číslo řádku, kde končí výběr.

**endColumn** – celé číslo sloupce v rámci na konci řádku, kde končí výběr.

Zobrazit [skriptování příklad](#scripting-example) dále v tomto tématu.

### <a name="selectcaretline"></a>SelectCaretLine\(\)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vybere celý řádek textu, který je v současné době obsahuje blikajícího kurzoru.

```powershell
# First, set the caret position on line 5.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
# Now select that entire line of text
$psISE.CurrentFile.Editor.SelectCaretLine()
```

### <a name="setcaretposition-linenumber-columnnumber-"></a>SetCaretPosition\( číslo řádku, columnNumber \)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Nastaví pozici blikajícího kurzoru na řádku číslo a číslo sloupce. Vyvolá výjimku, pokud je číslo řádku stříška nebo číslo sloupce blikající kurzor nedodržují jejich odpovídajících platné rozsahy.

**Číslo řádku** – celé číslo, číslo řádku blikajícího kurzoru.

**columnNumber** – celé číslo číslo sloupce blikajícího kurzoru.

```powershell
# Set the CaretPosition.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
```

### <a name="toggleoutliningexpansion"></a>ToggleOutliningExpansion\(\)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Způsobí, že všechny části osnovy rozbalit nebo sbalit.

```powershell
# Toggle the outlining expansion
$psISE.CurrentFile.Editor.ToggleOutliningExpansion()
```

## <a name="properties"></a>Properties

### <a name="cangotomatch"></a>CanGoToMatch

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Logická vlastnost jen pro čtení k určení, jestli je blikající kurzor vedle závorky, závorky nebo složenou závorku - \( \), \[ \], {}. Pokud kurzor se bezprostředně před počáteční znak nebo bezprostředně po koncový znak z dvojice, pak je tato hodnota vlastnosti **$true**. V opačném případě je **$false**.

```powershell
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psISE.CurrentFile.Editor.CanGoToMatch
```

### <a name="caretcolumn"></a>CaretColumn

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, který získá číslo sloupce, který odpovídá pozici blikajícího kurzoru.

```powershell
# Get the CaretColumn.
$psISE.CurrentFile.Editor.CaretColumn
```

### <a name="caretline"></a>CaretLine

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, která získá počet řádků, které obsahuje blikajícího kurzoru.

```powershell
# Get the CaretLine.
$psISE.CurrentFile.Editor.CaretLine
```

### <a name="caretlinetext"></a>CaretLineText

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, která vrací úplný řádek text, který obsahuje blikajícího kurzoru.

```powershell
# Get all of the text on the line that contains the caret.
$psISE.CurrentFile.Editor.CaretLineText
```

### <a name="linecount"></a>LineCount

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, která získá počet řádků v editoru.

```powershell
# Get the LineCount.
$psISE.CurrentFile.Editor.LineCount
```

### <a name="selectedtext"></a>SelectedText

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, která získá vybraný text z editoru.

Zobrazit [skriptování příklad](#scripting-example) dále v tomto tématu.

### <a name="text"></a>Text

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost pro čtení a zápis, která získá nebo nastaví text v editoru.

Zobrazit [skriptování příklad](#scripting-example) dále v tomto tématu.

## <a name="scripting-example"></a>Příklad skriptu

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

## <a name="see-also"></a>Viz také

- [Objekt ISEFile](The-ISEFile-Object.md)
- [Objekt PowerShellTab](The-PowerShellTab-Object.md)
- [Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)