---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt ISEEditor
ms.openlocfilehash: c593eeebf0b9a94769841efd2aa78f84a3829ca5
ms.sourcegitcommit: 3720ce4efb6735694cfb53a1b793d949af5d1bc5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2017
---
# <a name="the-iseeditor-object"></a>Objekt ISEEditor
  **ISEEditor** objekt je instance třídy Microsoft.PowerShell.Host.ISE.ISEEditor. V podokně konzole je **ISEEditor** objektu. Každý [ISEFile](The-ISEFile-Object.md) objektů má přidruženou **ISEEditor** objektu. V následujících částech jsou uvedené metody a vlastnosti **ISEEditor** objektu.

## <a name="methods"></a>Metody

### <a name="clear"></a>Zrušte zaškrtnutí\(\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vymaže text v editoru.

```powershell
# Clears the text in the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Clear()
```

### <a name="ensurevisibleint-linenumber"></a>EnsureVisible\(int lineNumber\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Posune editoru tak, aby řádek, který odpovídá zadané **lineNumber** hodnota parametru je viditelná. Ho vyvolá výjimku, pokud zadané číslo řádku je mimo rozsah 1, poslední číslo řádku, který definuje čísla platné řádků.

 **lineNumber** číslo řádku, který má být dostupná.

```powershell
# Scrolls the text in the Script pane so that the fifth line is in view. 
$psISE.CurrentFile.Editor.EnsureVisible(5)
```

### <a name="focus"></a>Fokus\(\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Nastaví fokus na editoru.

```powershell
# Sets focus to the Console pane. 
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### <a name="getlinelengthint-linenumber-"></a>GetLineLength\(int lineNumber\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Získá délku řádku jako celé číslo řádku, která je zadána číslo řádku.

 **lineNumber** číslo řádku, která se získat délku.

 **Vrátí** délka řádku pro řádek na číslo zadané.

```powershell
# Gets the length of the first line in the text of the Command pane. 
$psISE.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### <a name="gotomatch"></a>GoToMatch\(\)
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích. 

 Přesune vsuvka odpovídající znaku, pokud **CanGoToMatch** vlastností objektu editor je **$true**, která nastane, když pomocí kurzoru se bezprostředně před levé závorky, závorka nebo složené závorce - \(,\[, {- nebo ihned po uzavírací kulatá závorka, závorka nebo složené závorce - \),\],}.  Pomocí kurzoru je umístěna před znakem otevírání nebo po ukončovací znak. Pokud **CanGoToMatch** vlastnost je **$false**, pak tato metoda se nic nestane.

```powershell
# Test to see if the caret is next to a parenthesis, bracket, or brace.
```

### <a name="inserttext-text-"></a>InsertText\( textu\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Nahradí text výběr nebo vložení textu na aktuální pozici pomocí kurzoru.

 **text** -řetězec text, který chcete vložit.

 Najdete v článku [skriptování příklad](#scripting-example) dál v tomto tématu.

### <a name="select-startline-startcolumn-endline-endcolumn-"></a>Vyberte\( startLine, Hodnota startColumn, ukončovacího endColumn\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vybere text z **startLine**, **Hodnota startColumn**, **ukončovacího**, a **endColumn** parametry.

 **startLine** -celé číslo řádku, kde začíná výběr.

 **Hodnota startColumn** -celé číslo sloupce v řádku počáteční kde výběr spustí.

 **ukončovacího** -celé číslo řádku, které končí výběr.

 **endColumn** -celé číslo sloupce v rámci na konci řádku, které končí výběr.

 Najdete v článku [skriptování příklad](#scripting-example) dál v tomto tématu.

### <a name="selectcaretline"></a>SelectCaretLine\(\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vybere celý řádek text, který aktuálně obsahuje pomocí kurzoru.

```powershell
# First, set the caret position on line 5.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1) 
# Now select that entire line of text
$psISE.CurrentFile.Editor.SelectCaretLine()
```

### <a name="setcaretposition-linenumber-columnnumber-"></a>SetCaretPosition\( lineNumber čísla sloupce\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Nastavuje pozici pomocí kurzoru na řádku číslo a číslo sloupce. Ho vyvolá výjimku, pokud pomocí kurzoru číslo řádku nebo pomocí kurzoru číslo sloupce je mimo jejich příslušné platné rozsahy.

 **lineNumber** -celé číslo, číslo řádku pomocí kurzoru.

 **čísla sloupce** -celé číslo číslo sloupce pomocí kurzoru.

```powershell
# Set the CaretPosition.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
```

### <a name="toggleoutliningexpansion"></a>ToggleOutliningExpansion\(\)
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích. 

 Způsobí, že všechny části outline rozbalit nebo sbalit.

```powershell
# Toggle the outlining expansion
$psISE.CurrentFile.Editor.ToggleOutliningExpansion()
```

## <a name="properties"></a>Properties

### <a name="cangotomatch"></a>CanGoToMatch
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích. 

 Jen pro čtení vlastnost typu Boolean označující, zda pomocí kurzoru vedle závorky, závorka nebo složené závorce - \( \), \[ \], {}. Pokud pomocí kurzoru se bezprostředně před znak otevírání nebo bezprostředně po ukončovací znak pár, pak je tato hodnota vlastnosti **$true**. Jinak je **$false**.

```powershell
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psISE.CurrentFile.Editor.CanGoToMatch
```

### <a name="caretcolumn"></a>CaretColumn
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, který získá číslo sloupce, který odpovídá pozici pomocí kurzoru.

```powershell
# Get the CaretColumn.
$psISE.CurrentFile.Editor.CaretColumn
```

### <a name="caretline"></a>CaretLine
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, který získá číslo řádku, který obsahuje pomocí kurzoru.

```powershell
# Get the CaretLine.
$psISE.CurrentFile.Editor.CaretLine
```

### <a name="caretlinetext"></a>CaretLineText
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, který získá úplný řádek textu, který obsahuje pomocí kurzoru.

```powershell
# Get all of the text on the line that contains the caret.
$psISE.CurrentFile.Editor.CaretLineText
```

### <a name="linecount"></a>LineCount
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, získá počet řádků v editoru.

```powershell
# Get the LineCount.
$psISE.CurrentFile.Editor.LineCount
```

### <a name="selectedtext"></a>SelectedText
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, získá vybraný text v editoru.

 Najdete v článku [skriptování příklad](#scripting-example) dál v tomto tématu.

### <a name="text"></a>Text
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost pro čtení a zápis, který získá nebo nastaví text v editoru.

 Najdete v článku [skriptování příklad](#scripting-example) dál v tomto tématu.

## <a name="scripting-example"></a>Příklad skriptování

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
$endColumn= $myEditor.GetLineLength(3)
# Select the text in the first three lines.
$myEditor.Select(1,1,3,$endColumn + 1)
$selection = $myEditor.SelectedText
# Clear all the text in the editor.
$myEditor.Clear()
# Add the selected text back, but in lower case.
$myEditor.InsertText($selection.ToLower())
```

## <a name="see-also"></a>Viz také
- [Objekt ISEFile](The-ISEFile-Object.md) 
- [Objekt PowerShellTab](The-PowerShellTab-Object.md) 
- [ISE Windows PowerShell skriptování objektový Model](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Odkaz na objekt modelu Windows PowerShell ISE](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [Hierarchie ISE objektů modelu](The-ISE-Object-Model-Hierarchy.md)

  
