---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt ISEOptions
ms.assetid: 75e2a76f-f3d1-490b-ad5d-e3829946aabb
ms.openlocfilehash: 5e04adeebacfb9214bf39d9ec9c5f0e01f5729ee
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="the-iseoptions-object"></a>Objekt ISEOptions
  **ISEOptions** objekt představuje různá nastavení pro Windows PowerShell ISE. Je instance **Microsoft.PowerShell.Host.ISE.ISEOptions** třídy.

 **ISEOptions** objekt poskytuje následující metody a vlastnosti.

## <a name="methods"></a>Metody

### <a name="restoredefaultconsoletokencolors"></a>RestoreDefaultConsoleTokenColors\(\)
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Obnoví výchozí hodnoty tokenu barvy v podokně konzoly.

```
# Changes the color of the commands in the Console pane to red and then restores it to its default value.
$psISE.Options.ConsoleTokenColors["Command"] = "red"
$psISE.Options.RestoreDefaultConsoleTokenColors()
```

### <a name="restoredefaults"></a>RestoreDefaults\(\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Obnoví výchozí hodnoty nastavení možností v podokně konzoly. Obnoví také chování různých zprávy upozornění, které poskytují standardní zaškrtnutím políčka zabránit se znovu zobrazí zpráva.

```
# Changes the background color in the Console pane and then restores it to its default value.
$psISE.Options.ConsolePaneBackgroundColor = "orange"
$psISE.Options.RestoreDefaults()
```

### <a name="restoredefaulttokencolors"></a>RestoreDefaultTokenColors\(\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Obnoví výchozí hodnoty tokenu barvy v podokně skriptu.

```
# Changes the color of the comments in the Script pane to red and then restores it to its default value.
$psISE.Options.TokenColors["Comment"]="red"
$psISE.Options.RestoreDefaultTokenColors()
```

### <a name="restoredefaultxmltokencolors"></a>RestoreDefaultXmlTokenColors\(\)
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Obnoví výchozí hodnoty tokenu barvy pro elementy XML, které se zobrazují v systému Windows PowerShell ISE. Viz také [XmlTokenColors](#xmltokencolors).

```
# Changes the color of the comments in XML data to red and then restores it to its default value.
$psISE.Options.XmlTokenColors["Comment"]="red"
$psISE.Options.RestoreDefaultXmlTokenColors()
```

## <a name="properties"></a>Properties

### <a name="autosaveminuteinterval"></a>AutoSaveMinuteInterval
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje počet minut mezi operacemi automatického ukládání souborů pomocí Windows PowerShell ISE. Výchozí hodnota je 2 minut. Hodnota je celé číslo.

```
# Changes the number of minutes between automatic save operations to every 3 minutes.
$psISE.Options.AutoSaveMinuteInterval = 3
```

### <a name="commandpanebackgroundcolor"></a>CommandPaneBackgroundColor
  Tato funkce je k dispozici v prostředí Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.  Novější verze najdete v tématu [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).

 Určuje barvu pozadí pro příkaz podokně. Je instance **System.Windows.Media.Color** třídy.

```
# Changes the background color of the Command pane to orange.
$psISE.Options.CommandPaneBackgroundColor = "orange"
```

### <a name="commandpaneup"></a>CommandPaneUp
  Tato funkce je k dispozici v prostředí Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.

 Určuje, zda se nachází v podokně příkaz výše podokno výstup.

```
# Moves the Command pane to the top of the screen.
$psISE.Options.CommandPaneUp  = $true

```

### <a name="consolepanebackgroundcolor"></a>ConsolePaneBackgroundColor
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje barvu pozadí panelu konzoly. Je instance **System.Windows.Media.Color** třídy.

```
# Changes the background color of the Console pane to red.
$psISE.Options.ConsolePaneBackgroundColor = "red"
```

### <a name="consolepaneforegroundcolor"></a>ConsolePaneForegroundColor
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje barvu popředí textu v podokně konzoly.

```
# Changes the foreground color of the text in the Console pane to yellow.
$psISE.Options.ConsolePaneForegroundColor  = "yellow"

```

### <a name="consolepanetextbackgroundcolor"></a>ConsolePaneTextBackgroundColor
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje barvu pozadí textu v podokně konzoly.

```
# Changes the background color of the Console pane text to pink.
$psISE.Options.ConsolePaneTextBackgroundColor = "pink"
```

### <a name="consoletokencolors"></a>ConsoleTokenColors
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje barvy tokenů IntelliSense v podokně konzoly ISE Windows PowerShell. Tato vlastnost je objekt slovník, který obsahuje dvojice název/hodnota pro typy tokenů a barvy pro podokně konzoly. Chcete-li změnit barvy tokenů IntelliSense v podokně skriptu, [TokenColors](#tokencolors). Barvy resetovat na výchozí hodnoty, najdete v části [RestoreDefaultConsoleTokenColors](#restoredefaultconsoletokencolors). Token barvy lze nastavit pro následující: atribut, příkazu, CommandArgument, CommandParameter, komentáře, GroupEnd, GroupStart, – klíčové slovo, LineContinuation, LoopLabel, člen, nový řádek, číslo, operátor, pozice, StatementSeparator, řetězec, typ, Neznámá, proměnné.

```
# Sets the color of commands to green.
$psISE.Options.ConsoleTokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.ConsoleTokenColors["Keyword"] = "magenta"

```

### <a name="debugbackgroundcolor"></a>DebugBackgroundColor
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Určuje barvu pozadí pro ladění text, který se zobrazí v podokně konzoly. Je instance **System.Windows.Media.Color** třídy.

```
# Changes the background color for the debug text that appears in the Console pane to blue.
$psISE.Options.DebugBackgroundColor ='#0000FF'
```

### <a name="debugforegroundcolor"></a>DebugForegroundColor
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Určuje barvu popředí pro ladění text, který se zobrazí v podokně konzoly. Je instance **System.Windows.Media.Color** třídy.

```
# Changes the foreground color for the debug text that appears in the Console pane to yellow.
$psISE.Options.DebugForegroundColor ="yellow"
```

### <a name="defaultoptions"></a>DefaultOptions
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Kolekce vlastností, které určují, které se používají při resetování metody se používají výchozí hodnoty.

```
# Displays the name of the default options. This example is from ISE 4.0.
$psISE.Options.DefaultOptions

SelectedScriptPaneState                   : Top
ShowDefaultSnippets                       : True
ShowToolBar                               : True
ShowOutlining                             : True
ShowLineNumbers                           : True
TokenColors                               : {[Attribute, #FF00BFFF], [Command, #FF0000FF], [CommandArgument, #FF8A2BE2], [CommandParameter, #FF000080]...}
ConsoleTokenColors                        : {[Attribute, #FFB0C4DE], [Command, #FFE0FFFF], [CommandArgument, #FFEE82EE], [CommandParameter, #FFFFE4B5]...}
XmlTokenColors                            : {[Comment, #FF006400], [CommentDelimiter, #FF008000], [ElementName, #FF8B0000], [MarkupExtension, #FFFF8C00]...}
DefaultOptions                            : Microsoft.PowerShell.Host.ISE.ISEOptions
FontSize                                  : 9
Zoom                                      : 100
FontName                                  : Lucida Console
ErrorForegroundColor                      : #FFFF0000
ErrorBackgroundColor                      : #00FFFFFF
WarningForegroundColor                    : #FFFF8C00
WarningBackgroundColor                    : #00FFFFFF
VerboseForegroundColor                    : #FF00FFFF
VerboseBackgroundColor                    : #00FFFFFF
DebugForegroundColor                      : #FF00FFFF
DebugBackgroundColor                      : #00FFFFFF
ConsolePaneBackgroundColor                : #FF012456
ConsolePaneTextBackgroundColor            : #FF012456
ConsolePaneForegroundColor                : #FFF5F5F5
ScriptPaneBackgroundColor                 : #FFFFFFFF
ScriptPaneForegroundColor                 : #FF000000
ShowWarningForDuplicateFiles              : True
ShowWarningBeforeSavingOnRun              : True
UseLocalHelp                              : True
AutoSaveMinuteInterval                    : 2
MruCount                                  : 10
ShowIntellisenseInConsolePane             : True
ShowIntellisenseInScriptPane              : True
UseEnterToSelectInConsolePaneIntellisense : True
UseEnterToSelectInScriptPaneIntellisense  : True
IntellisenseTimeoutInSeconds              : 3

```

### <a name="errorbackgroundcolor"></a>ErrorBackgroundColor
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Určuje barvu pozadí pro text chyby, který se zobrazí v podokně konzoly. Je instance **System.Windows.Media.Color** třídy.

```
# Changes the background color for the error text that appears in the Console pane to black.
$psISE.Options.ErrorBackgroundColor="black"
```

### <a name="errorforegroundcolor"></a>ErrorForegroundColor
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Určuje barvu popředí pro text chyby, který se zobrazí v podokně konzoly. Je instance **System.Windows.Media.Color** třídy.

```
# Changes the foreground color for the error text that appears in the console pane to green.
$psISE.Options.ErrorForegroundColor ="green"
```

### <a name="fontname"></a>Název písma
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Určuje název písma aktuálně používá v podokně skriptu a v podokně konzoly.

```
# Changes the font used in both panes.
$psISE.Options.FontName = "courier new"
```

### <a name="fontsize"></a>Velikost písma
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Určuje velikost písma jako celé číslo. Používá se v podokně skriptu, příkaz podokně a podokně výstup. Platný rozsah hodnot je 8 až 32.

```
# Changes the font size in all panes.
$psISE.Options.FontSize = 20

```

### <a name="intellisensetimeoutinseconds"></a>IntellisenseTimeoutInSeconds
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje počet sekund, po které IntelliSense používá k řešení aktuálně zadaný text. Po tomto počtu sekund IntelliSense vyprší časový limit a umožňuje pokračujte v zadávání. Výchozí hodnota je 3 sekund. Hodnota je celé číslo.

```
# Changes the number of seconds for IntelliSense syntax recognition to 5.
$psISE.Options.IntellisenseTimeoutInSeconds = 5
```

### <a name="mrucount"></a>MruCount
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje počet posledních otevřených souborů, které Windows PowerShell ISE sleduje a zobrazí se v dolní části **otevřít soubor** nabídky. Výchozí hodnota je 10. Hodnota je celé číslo.

```
# Changes the number of recently used files that appear at the bottom of the File Open menu to 5.
$psISE.Options.MruCount = 5
```

### <a name="outputpanebackgroundcolor"></a>OutputPaneBackgroundColor
  Tato funkce je k dispozici v prostředí Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.  Novější verze najdete v tématu [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).

 Vlastnost pro čtení a zápis, získá nebo nastaví barvu pozadí pro podokno výstup sám sebe. Je instance **System.Windows.Media.Color** třídy.

```
# Changes the background color of the Output pane to gold.
$psISE.Options.OutputPaneForegroundColor = "gold"

```

### <a name="outputpanetextforegroundcolor"></a>OutputPaneTextForegroundColor
  Tato funkce je k dispozici v prostředí Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.  Novější verze najdete v tématu [ConsolePaneForegroundColor](#consolepaneforegroundcolor).

 Vlastnost pro čtení a zápis, který změní barvu popředí textu v podokně výstup v prostředí Windows PowerShell ISE 2.0.

```
# Changes the foreground color of the text in the Output Pane to blue.
$psISE.Options.OutputPaneTextForegroundColor  = "blue"

```

### <a name="outputpanetextbackgroundcolor"></a>OutputPaneTextBackgroundColor
  Tato funkce je k dispozici v prostředí Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.  Novější verze najdete v tématu [ConsolePaneTextBackgroundColor](#consolepanetextbackgroundcolor).

 Vlastnost pro čtení a zápis, která změní barvu pozadí textu v podokně výstup.

```
# Changes the background color of the Output pane text to pink.
$psISE.Options.OutputPaneTextBackgroundColor = "pink"
```

### <a name="scriptpanebackgroundcolor"></a>ScriptPaneBackgroundColor
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Vlastnost pro čtení a zápis, který získá nebo nastaví barvu pozadí pro soubory. Je instance **System.Windows.Media.Color** třídy.

```

# Sets the color of the script pane background to yellow.
$psISE.Options.ScriptPaneBackgroundColor = 'yellow'

```

### <a name="scriptpaneforegroundcolor"></a>ScriptPaneForegroundColor
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Vlastnost pro čtení a zápis, který získá nebo nastaví barvu popředí pro soubory bez skriptu v podokně skriptu.
Pokud chcete nastavit barvu popředí pro soubory skriptu, použijte [TokenColors](#tokencolors).

```
# Sets the foreground to color of non-script files in the script pane to green.
$psISE.Options.ScriptPaneBackgroundColor = "green"

```

### <a name="selectedscriptpanestate"></a>SelectedScriptPaneState
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Vlastnost pro čtení a zápis, získá nebo nastaví pozici v podokně skriptu na zobrazení. Může být řetězec "Maximized", "Top" nebo "Vpravo".

```
# Moves the Script Pane to the top.
$psISE.Options.SelectedScriptPaneState = "Top"
# Moves the Script Pane to the right.
$psISE.Options.SelectedScriptPaneState = "Right"
# Maximizes the Script Pane
$psISE.Options.SelectedScriptPaneState = "Maximized"

```

### <a name="showdefaultsnippets"></a>ShowDefaultSnippets
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje, zda **CTRL + J** seznam fragmenty obsahuje sadu starter, který je součástí prostředí Windows PowerShell. Pokud nastavíte hodnotu **$false**, se zobrazí pouze fragmenty uživatelem definované v **CTRL + J** seznamu. Výchozí hodnota je **$true**.

```
# Hide the default snippets from the CTRL+J list.
$psISe.Options.ShowDefaultSnippets = $false
```

### <a name="showintellisenseinconsolepane"></a>ShowIntellisenseInConsolePane
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje, zda IntelliSense nabízí syntaxi parametru a hodnota návrhy v podokně konzoly. Výchozí hodnota je **$true**.

```
# Turn off IntelliSense in the console pane.
$psISe.Options.ShowIntellisenseInConsolePane = $false
```

### <a name="showintellisenseinscriptpane"></a>ShowIntellisenseInScriptPane
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje, zda IntelliSense nabízí syntaxi parametru a hodnota návrhy v podokně skriptu. Výchozí hodnota je **$true**.

```
# Turn off IntelliSense in the Script pane.
$psISe.Options.ShowIntellisenseInScriptPane = $false
```

### <a name="showlinenumbers"></a>ShowLineNumbers
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje, zda v podokně skriptu se zobrazí na levém okraji čísla řádků. Výchozí hodnota je **$true**.

```
# Turn off line numbers in the Script pane.
$psISe.Options.ShowLineNumbers = $false
```

### <a name="showoutlining"></a>ShowOutlining
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje, zda v podokně skriptu se zobrazí na levém okraji rozšíření a sbalitelné závorky vedle sekcí kódu. Pokud jsou zobrazeny, můžete kliknout na minus \( - \) ikonami vedle blok textu sbalit, nebo kliknutím na tlačítko plus \( + \) ikonu rozbalte blok textu. Výchozí hodnota je **$true**.

```
# Turn off outlining in the Script pane.
$psISe.Options.ShowOutlining = $false
```

### <a name="showtoolbar"></a>ShowToolbar –
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Určuje, zda se zobrazí panelu nástrojů (ISE) v horní části okna Windows PowerShell ISE. Výchozí hodnota je **$true**.

```
# Show the toolbar.
$psISe.Options.ShowToolBar = $true
```

### <a name="showwarningbeforesavingonrun"></a>ShowWarningBeforeSavingOnRun
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Určuje, zda zpráva upozornění se zobrazí, když skriptu se automaticky uloží, než je spuštěn. Výchozí hodnota je **$true**.

```
# Enable the warning message when an attempt
# is made to run a script without saving it first.
$psISE.Options.ShowWarningBeforeSavingOnRun=$true

```

### <a name="showwarningforduplicatefiles"></a>ShowWarningForDuplicateFiles
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Určuje, zda zpráva upozornění se zobrazí, když je stejný soubor otevřít na různých záložkách prostředí PowerShell. Pokud nastavena na **$true**, stejný soubor otevřete v několika karty zobrazí tato zpráva: "kopii tohoto souboru je otevřen v jiné kartě prostředí Windows PowerShell. Změny provedené v tomto souboru bude mít vliv na všechny otevřené kopie." Výchozí hodnota je **$true**.

```
# Enable the warning message when a file is
# opened in multiple PowerShell tabs.
$psISE.Options.ShowWarningForDuplicateFiles = $true

```

### <a name="tokencolors"></a>TokenColors
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Určuje barvy tokenů IntelliSense v podokně skript prostředí Windows PowerShell ISE. Tato vlastnost je objekt slovník, který obsahuje dvojice název/hodnota pro typy tokenů a barvy pro podokně skriptu. Chcete-li změnit barvy tokenů IntelliSense v podokně konzoly, [ConsoleTokenColors](#consoletokencolors). Barvy resetovat na výchozí hodnoty, najdete v části [RestoreDefaultTokenColors](#restoredefaulttokencolors). Token barvy lze nastavit pro následující: atribut, příkazu, CommandArgument, CommandParameter, komentáře, GroupEnd, GroupStart, – klíčové slovo, LineContinuation, LoopLabel, člen, nový řádek, číslo, operátor, pozice, StatementSeparator, řetězec, typ, Neznámá, proměnné.

```
# Sets the color of commands to green.
$psISE.Options.TokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.TokenColors["Keyword"] = "magenta"

```

### <a name="useentertoselectinconsolepaneintellisense"></a>UseEnterToSelectInConsolePaneIntellisense
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje, zda můžete použít klávesu Enter a vyberte IntelliSense poskytuje možnost v podokně konzoly. Výchozí hodnota je **$true**.

```
# Turn off using the ENTER key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense=$false

```

### <a name="useentertoselectinscriptpaneintellisense"></a>UseEnterToSelectInScriptPaneIntellisense
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje, zda můžete použít klávesu Enter a vyberte možnost zadaný IntelliSense v podokně skriptu. Výchozí hodnota je **$true**.

```
# Turn on using the Enter key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense=$true

```

### <a name="uselocalhelp"></a>UseLocalHelp
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje, zda lokálně nainstalované nápovědy nebo online knihovně TechNet nápovědy se zobrazí po stisknutí klávesy F1 umístěte kurzor v klíčové slovo. Pokud nastavena na **$true**, pak automaticky otevírané okno zobrazuje obsahu pomocí lokálně nainstalované nápovědy. Soubory nápovědy můžete nainstalovat spuštěním `Update-Help` příkaz. Pokud nastavena na **$false**, pak otevře prohlížeč na stránku v knihovně TechNet.

```
# Sets the option for the online help to be displayed.
$psISE.Options.UseLocalHelp=$false
# Sets the option for the local Help to be displayed.
$psISE.Options.UseLocalHelp=$true

```

### <a name="verbosebackgroundcolor"></a>VerboseBackgroundColor
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Určuje barvu pozadí pro podrobné text, který se zobrazí v podokně konzoly. Je **System.Windows.Media.Color** objektu.

```
# Changes the background color for verbose text to blue.
$psISE.Options.VerboseBackgroundColor ='#0000FF'
```

### <a name="verboseforegroundcolor"></a>VerboseForegroundColor
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Určuje barvu popředí pro podrobné text, který se zobrazí v podokně konzoly. Je **System.Windows.Media.Color** objektu.

```
# Changes the foreground color for verbose text to yellow.
$psISE.Options.VerboseForegroundColor ='yellow'
```

### <a name="warningbackgroundcolor"></a>WarningBackgroundColor
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Určuje barvu pozadí pro upozornění text, který se zobrazí v podokně konzoly. Je **System.Windows.Media.Color** objektu.

```
# Changes the background color for warning text to blue.
$psISE.Options.WarningBackgroundColor ='#0000FF'
```

### <a name="warningforegroundcolor"></a>WarningForegroundColor
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Určuje barvu popředí pro upozornění text, který se zobrazí v podokně výstup. Je **System.Windows.Media.Color** objektu.

```
# Changes the foreground color for warning text to yellow.
$psISE.Options.WarningForegroundColor ='yellow'
```

### <a name="xmltokencolors"></a>XmlTokenColors
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje objekt slovník, který obsahuje dvojice název/hodnota pro typy tokenů a barvy pro obsah XML, který se zobrazí v systému Windows PowerShell ISE. Token barvy lze nastavit pro následující: atribut, příkazu, CommandArgument, CommandParameter, komentáře, GroupEnd, GroupStart, – klíčové slovo, LineContinuation, LoopLabel, člen, nový řádek, číslo, operátor, pozice, StatementSeparator, řetězec, typ, Neznámá, proměnné. Viz také [RestoreDefaultXmlTokenColors](#restoredefaultxmltokencolors).

```
# Sets the color of XML element names to green.
$psISE.Options.XmlTokenColors["ElementName"] = "green"
# Sets the color of XML comments to magenta.
$psISE.Options.XmlTokenColors["Comment"] = "magenta"

```

### <a name="zoom"></a>Přiblížení
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Určuje relativní velikost textu v konzole i skriptu podokna. Výchozí hodnota je 100. Menší hodnoty způsobit, že text v systému Windows PowerShell ISE zobrazí menší při větší počty způsobit text, který se zobrazí větší. Hodnota je celé číslo, které se pohybuje od 20 do 400.

```
# Changes the text in the Windows PowerShell ISE to be double its normal size.
$psISE.Options.Zoom = 200
```

## <a name="see-also"></a>Viz také
- [ISE Windows PowerShell skriptování objektový Model](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Odkaz na objekt modelu Windows PowerShell ISE](Windows-PowerShell-ISE-Object-Model-Reference.md)

