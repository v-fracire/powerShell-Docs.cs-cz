---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEOptions
ms.assetid: 75e2a76f-f3d1-490b-ad5d-e3829946aabb
ms.openlocfilehash: e756da21aaa5465f7fa6a90563b4180f0c89e87b
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404040"
---
# <a name="the-iseoptions-object"></a>Objekt ISEOptions

**ISEOptions** objekt představuje různá nastavení pro Windows PowerShell ISE. Je instancí **Microsoft.PowerShell.Host.ISE.ISEOptions** třídy.

**ISEOptions** objekt, který poskytuje následující metody a vlastnosti.

## <a name="methods"></a>Metody

### <a name="restoredefaultconsoletokencolors"></a>RestoreDefaultConsoleTokenColors\(\)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Obnoví výchozí hodnoty tokenu barvy v podokně konzoly.

```powershell
# Changes the color of the commands in the Console pane to red and then restores it to its default value.
$psISE.Options.ConsoleTokenColors["Command"] = 'red'
$psISE.Options.RestoreDefaultConsoleTokenColors()
```

### <a name="restoredefaults"></a>RestoreDefaults\(\)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Obnoví výchozí hodnoty všech nastavení možnosti v podokně konzoly. Obnoví také chování různých varovné zprávy, které poskytují standardní zaškrtnutím políčka zabránit znovu zobrazí zpráva.

```powershell
# Changes the background color in the Console pane and then restores it to its default value.
$psISE.Options.ConsolePaneBackgroundColor = 'orange'
$psISE.Options.RestoreDefaults()
```

### <a name="restoredefaulttokencolors"></a>RestoreDefaultTokenColors\(\)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Obnoví výchozí hodnoty tokenu barvy v podokně skriptu.

```powershell
# Changes the color of the comments in the Script pane to red and then restores it to its default value.
$psISE.Options.TokenColors["Comment"] = 'red'
$psISE.Options.RestoreDefaultTokenColors()
```

### <a name="restoredefaultxmltokencolors"></a>RestoreDefaultXmlTokenColors\(\)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Obnoví výchozí hodnoty tokenu barev pro prvky, které jsou zobrazeny v prostředí Windows PowerShell ISE. Viz také [XmlTokenColors](#xmltokencolors).

```powershell
# Changes the color of the comments in XML data to red and then restores it to its default value.
$psISE.Options.XmlTokenColors["Comment"] = 'red'
$psISE.Options.RestoreDefaultXmlTokenColors()
```

## <a name="properties"></a>Properties

### <a name="autosaveminuteinterval"></a>AutoSaveMinuteInterval

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje počet minut mezi operacemi automatického ukládání souborů ve Windows PowerShell ISE. Výchozí hodnota je 2 minuty. Hodnota je celé číslo.

```powershell
# Changes the number of minutes between automatic save operations to every 3 minutes.
$psISE.Options.AutoSaveMinuteInterval = 3
```

### <a name="commandpanebackgroundcolor"></a>CommandPaneBackgroundColor

Tato funkce je k dispozici v rozhraní Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.  Novější verze, najdete v části [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).

Určuje barvu pozadí v příkazovém podokně. Je instancí **System.Windows.Media.Color** třídy.

```powershell
# Changes the background color of the Command pane to orange.
$psISE.Options.CommandPaneBackgroundColor = 'orange'
```

### <a name="commandpaneup"></a>CommandPaneUp

Tato funkce je k dispozici v rozhraní Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.

Určuje, zda v příkazovém podokně se nachází nad podokno výstup.

```powershell
# Moves the Command pane to the top of the screen.
$psISE.Options.CommandPaneUp  = $true
```

### <a name="consolepanebackgroundcolor"></a>ConsolePaneBackgroundColor

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje barvu pozadí panelu konzoly. Je instancí **System.Windows.Media.Color** třídy.

```powershell
# Changes the background color of the Console pane to red.
$psISE.Options.ConsolePaneBackgroundColor = 'red'
```

### <a name="consolepaneforegroundcolor"></a>ConsolePaneForegroundColor

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje barvu popředí textu na panelu konzoly.

```powershell
# Changes the foreground color of the text in the Console pane to yellow.
$psISE.Options.ConsolePaneForegroundColor  = 'yellow'
```

### <a name="consolepanetextbackgroundcolor"></a>ConsolePaneTextBackgroundColor

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje barvu pozadí textu v podokně konzoly.

```powershell
# Changes the background color of the Console pane text to pink.
$psISE.Options.ConsolePaneTextBackgroundColor = 'pink'
```

### <a name="consoletokencolors"></a>ConsoleTokenColors

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje barvy tokenů technologie IntelliSense v podokně konzoly ISE Windows Powershellu. Tato vlastnost je objekt slovníku obsahující dvojice název/hodnota pro typy tokenů a barvy v podokně konzoly. Chcete-li změnit barvy IntelliSense tokeny z podokna skriptu, [TokenColors](#tokencolors). Barvy resetovat na výchozí hodnoty, najdete v článku [RestoreDefaultConsoleTokenColors](#restoredefaultconsoletokencolors). Token barev můžete nastavit pro následující: Atribut, příkaz, CommandArgument, CommandParameter, komentáře, GroupEnd, GroupStart, – klíčové slovo, LineContinuation, LoopLabel, člen, nový řádek, číslo, – operátor, pozice, StatementSeparator, řetězec, typ, neznámý, proměnné.

```powershell
# Sets the color of commands to green.
$psISE.Options.ConsoleTokenColors["Command"] = 'green'
# Sets the color of keywords to magenta.
$psISE.Options.ConsoleTokenColors["Keyword"] = 'magenta'
```

### <a name="debugbackgroundcolor"></a>DebugBackgroundColor

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Určuje barvu pozadí pro ladění text, který se zobrazí v podokně konzoly. Je instancí **System.Windows.Media.Color** třídy.

```powershell
# Changes the background color for the debug text that appears in the Console pane to blue.
$psISE.Options.DebugBackgroundColor = '#0000FF'
```

### <a name="debugforegroundcolor"></a>DebugForegroundColor

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Určuje barvu popředí pro ladění text, který se zobrazí v podokně konzoly. Je instancí **System.Windows.Media.Color** třídy.

```powershell
# Changes the foreground color for the debug text that appears in the Console pane to yellow.
$psISE.Options.DebugForegroundColor = 'yellow'
```

### <a name="defaultoptions"></a>DefaultOptions

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Kolekce vlastností, které určují výchozí hodnoty, která se použije při resetování metody se používají.

```powershell
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

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Určuje barvu pozadí pro text chyby, které se zobrazí v podokně konzoly. Je instancí **System.Windows.Media.Color** třídy.

```powershell
# Changes the background color for the error text that appears in the Console pane to black.
$psISE.Options.ErrorBackgroundColor = 'black'
```

### <a name="errorforegroundcolor"></a>ErrorForegroundColor

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Určuje barvu popředí pro text chyby, které se zobrazí v podokně konzoly. Je instancí **System.Windows.Media.Color** třídy.

```powershell
# Changes the foreground color for the error text that appears in the console pane to green.
$psISE.Options.ErrorForegroundColor = 'green'
```

### <a name="fontname"></a>Název písma

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Určuje název písma aktuálně používá v podokně skriptu a v podokně konzoly.

```powershell
# Changes the font used in both panes.
$psISE.Options.FontName = 'Courier New'
```

### <a name="fontsize"></a>Velikost písma

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Určuje velikost písma jako celé číslo. Používá se v podokně skriptu, příkazovém podokně a podokně výstup. Platný rozsah hodnot je 8 až 32.

```powershell
# Changes the font size in all panes.
$psISE.Options.FontSize = 20
```

### <a name="intellisensetimeoutinseconds"></a>IntellisenseTimeoutInSeconds

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje počet sekund, které používá technologii IntelliSense pro pokus o vyřešení aktuálně zadaný text. Technologie IntelliSense po tomto počtu sekund, vyprší časový limit a umožňuje pokračovat v zadávání. Výchozí hodnota je 3 sekundy. Hodnota je celé číslo.

```powershell
# Changes the number of seconds for IntelliSense syntax recognition to 5.
$psISE.Options.IntellisenseTimeoutInSeconds = 5
```

### <a name="mrucount"></a>MruCount

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje počet naposledy otevřených souborů, které Windows PowerShell ISE sleduje a zobrazí v dolní části **otevřít soubor** nabídky. Výchozí hodnota je 10. Hodnota je celé číslo.

```powershell
# Changes the number of recently used files that appear at the bottom of the File Open menu to 5.
$psISE.Options.MruCount = 5
```

### <a name="outputpanebackgroundcolor"></a>OutputPaneBackgroundColor

Tato funkce je k dispozici v rozhraní Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.  Novější verze, najdete v části [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).

Čtení a zápis vlastnost, která získá nebo nastaví barvu pozadí pro podokno výstup samotný. Je instancí **System.Windows.Media.Color** třídy.

```powershell
# Changes the background color of the Output pane to gold.
$psISE.Options.OutputPaneForegroundColor = 'gold'
```

### <a name="outputpanetextforegroundcolor"></a>OutputPaneTextForegroundColor

Tato funkce je k dispozici v rozhraní Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.  Novější verze, najdete v části [ConsolePaneForegroundColor](#consolepaneforegroundcolor).

Vlastnost pro čtení a zápis, která změní barvu popředí textu v podokně výstupů v rozhraní Windows PowerShell ISE 2.0.

```powershell
# Changes the foreground color of the text in the Output Pane to blue.
$psISE.Options.OutputPaneTextForegroundColor  = 'blue'
```

### <a name="outputpanetextbackgroundcolor"></a>OutputPaneTextBackgroundColor

Tato funkce je k dispozici v rozhraní Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.  Novější verze, najdete v části [ConsolePaneTextBackgroundColor](#consolepanetextbackgroundcolor).

Vlastnost pro čtení a zápis, která změní barvu pozadí textu v podokně výstup.

```powershell
# Changes the background color of the Output pane text to pink.
$psISE.Options.OutputPaneTextBackgroundColor = 'pink'
```

### <a name="scriptpanebackgroundcolor"></a>ScriptPaneBackgroundColor

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost pro čtení a zápis, která získá nebo nastaví barvu pozadí pro soubory. Je instancí **System.Windows.Media.Color** třídy.

```powershell
# Sets the color of the script pane background to yellow.
$psISE.Options.ScriptPaneBackgroundColor = 'yellow'
```

### <a name="scriptpaneforegroundcolor"></a>ScriptPaneForegroundColor

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Čtení a zápis vlastnost, která získá nebo nastaví barvu popředí pro soubory bez skriptů, v podokně skriptu.
Chcete-li nastavit barvu popředí pro soubory skriptu, použijte [TokenColors](#tokencolors).

```powershell
# Sets the foreground to color of non-script files in the script pane to green.
$psISE.Options.ScriptPaneBackgroundColor = 'green'
```

### <a name="selectedscriptpanestate"></a>SelectedScriptPaneState

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost pro čtení a zápis, která získává nebo nastavuje pozici v podokně skriptu na displeji. Řetězec může být 'Maximized', 'Top' nebo 'Right'.

```powershell
# Moves the Script Pane to the top.
$psISE.Options.SelectedScriptPaneState = 'Top'
# Moves the Script Pane to the right.
$psISE.Options.SelectedScriptPaneState = 'Right'
# Maximizes the Script Pane
$psISE.Options.SelectedScriptPaneState = 'Maximized'
```

### <a name="showdefaultsnippets"></a>ShowDefaultSnippets

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje, zda **CTRL + J** fragmenty patří sady starter, který je součástí prostředí Windows PowerShell. Pokud je nastavena na **$false**, pouze uživatelské fragmentů se nachází v **CTRL + J** seznamu. Výchozí hodnota je **$true**.

```powershell
# Hide the default snippets from the CTRL+J list.
$psISE.Options.ShowDefaultSnippets = $false
```

### <a name="showintellisenseinconsolepane"></a>ShowIntellisenseInConsolePane

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje, zda IntelliSense nabízí syntaxe, parametrů a hodnotu návrhů v podokně konzoly. Výchozí hodnota je **$true**.

```powershell
# Turn off IntelliSense in the console pane.
$psISE.Options.ShowIntellisenseInConsolePane = $false
```

### <a name="showintellisenseinscriptpane"></a>ShowIntellisenseInScriptPane

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje, zda IntelliSense nabízí návrhy hodnotu z podokna skriptu, syntaxi a parametr. Výchozí hodnota je **$true**.

```powershell
# Turn off IntelliSense in the Script pane.
$psISE.Options.ShowIntellisenseInScriptPane = $false
```

### <a name="showlinenumbers"></a>Showlinenumberszobrazitčíslařádků

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje, zda v podokně skriptu se zobrazí na levém okraji čísla řádků. Výchozí hodnota je **$true**.

```powershell
# Turn off line numbers in the Script pane.
$psISE.Options.ShowLineNumbers = $false
```

### <a name="showoutlining"></a>ShowOutlining

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje, zda v podokně skriptu se zobrazí rozšiřitelná a sbalitelný závorkách vedle části kódu na levém okraji. Při jejich zobrazení, můžete kliknout na minus \( - \) ikonami vedle jejich blok textu sbalit, nebo klikněte na znaménko plus \( + \) ikony blok textu. Výchozí hodnota je **$true**.

```powershell
# Turn off outlining in the Script pane.
$psISE.Options.ShowOutlining = $false
```

### <a name="showtoolbar"></a>ShowToolbar –

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Určuje, zda ISE nástrojů se zobrazí v horní části okna Windows PowerShell ISE. Výchozí hodnota je **$true**.

```powershell
# Show the toolbar.
$psISE.Options.ShowToolBar = $true
```

### <a name="showwarningbeforesavingonrun"></a>ShowWarningBeforeSavingOnRun

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Určuje, zda se při skriptu je automaticky uložen před spuštěním zobrazí zpráva s upozorněním. Výchozí hodnota je **$true**.

```powershell
# Enable the warning message when an attempt
# is made to run a script without saving it first.
$psISE.Options.ShowWarningBeforeSavingOnRun = $true
```

### <a name="showwarningforduplicatefiles"></a>ShowWarningForDuplicateFiles

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Určuje, zda se při otevření stejného souboru na různých záložkách Powershellu zobrazí upozornění. Pokud hodnotu **$true**, stejný soubor otevřete v několika karet zobrazí tato zpráva: "Kopii tohoto souboru je otevřít na jiné kartě prostředí Windows PowerShell. Změny provedené pro tento soubor bude mít vliv na všechny otevřené kopie." Výchozí hodnota je **$true**.

```powershell
# Enable the warning message when a file is
# opened in multiple PowerShell tabs.
$psISE.Options.ShowWarningForDuplicateFiles = $true
```

### <a name="tokencolors"></a>TokenColors

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

V podokně skriptu Windows PowerShell ISE určuje barvy tokenů technologie IntelliSense. Tato vlastnost je objekt slovníku obsahující dvojice název/hodnota pro typy tokenů a barvy v podokně skriptu. Chcete-li změnit barvy tokeny technologie IntelliSense v podokně konzoly, [ConsoleTokenColors](#consoletokencolors). Barvy resetovat na výchozí hodnoty, najdete v článku [RestoreDefaultTokenColors](#restoredefaulttokencolors). Token barev můžete nastavit pro následující: Atribut, příkaz, CommandArgument, CommandParameter, komentáře, GroupEnd, GroupStart, – klíčové slovo, LineContinuation, LoopLabel, člen, nový řádek, číslo, – operátor, pozice, StatementSeparator, řetězec, typ, neznámý, proměnné.

```powershell
# Sets the color of commands to green.
$psISE.Options.TokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.TokenColors["Keyword"] = "magenta"
```

### <a name="useentertoselectinconsolepaneintellisense"></a>UseEnterToSelectInConsolePaneIntellisense

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje, zda můžete použít klávesu Enter k výběru informace IntelliSense poskytované v podokně konzoly. Výchozí hodnota je **$true**.

```powershell
# Turn off using the ENTER key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense = $false
```

### <a name="useentertoselectinscriptpaneintellisense"></a>UseEnterToSelectInScriptPaneIntellisense

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje, zda můžete použít klávesu Enter pro výběr možnosti poskytované technologie IntelliSense v podokně skriptu. Výchozí hodnota je **$true**.

```powershell
# Turn on using the Enter key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense = $true
```

### <a name="uselocalhelp"></a>UseLocalHelp

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje, zda místně instalované pomoc nebo online knihovně TechNet pomoct se zobrazí, když stisknete klávesu F1 s kurzorem umístěným v určitém klíčovém slově. Pokud hodnotu **$true**, pak automaticky otevíraném okně zobrazí obsahu z místně instalované nápovědy. Soubory nápovědy můžete nainstalovat spuštěním `Update-Help` příkazu. Pokud hodnotu **$false**, pak prohlížeči se otevře stránka v knihovně TechNet.

```powershell
# Sets the option for the online help to be displayed.
$psISE.Options.UseLocalHelp = $false
# Sets the option for the local Help to be displayed.
$psISE.Options.UseLocalHelp = $true
```

### <a name="verbosebackgroundcolor"></a>VerboseBackgroundColor

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Určuje barvu pozadí pro podrobné text, který se zobrazí v podokně konzoly. Jde **System.Windows.Media.Color** objektu.

```powershell
# Changes the background color for verbose text to blue.
$psISE.Options.VerboseBackgroundColor ='#0000FF'
```

### <a name="verboseforegroundcolor"></a>VerboseForegroundColor

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Určuje barvu popředí pro podrobné text, který se zobrazí v podokně konzoly. Jde **System.Windows.Media.Color** objektu.

```powershell
# Changes the foreground color for verbose text to yellow.
$psISE.Options.VerboseForegroundColor = 'yellow'
```

### <a name="warningbackgroundcolor"></a>WarningBackgroundColor

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Určuje barvu pozadí pro text upozornění, která se zobrazí v podokně konzoly. Jde **System.Windows.Media.Color** objektu.

```powershell
# Changes the background color for warning text to blue.
$psISE.Options.WarningBackgroundColor = '#0000FF'
```

### <a name="warningforegroundcolor"></a>WarningForegroundColor

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Určuje barvu popředí pro text upozornění, která se zobrazí v podokně výstup. Jde **System.Windows.Media.Color** objektu.

```powershell
# Changes the foreground color for warning text to yellow.
$psISE.Options.WarningForegroundColor = 'yellow'
```

### <a name="xmltokencolors"></a>XmlTokenColors

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje objekt slovníku obsahující dvojice název/hodnota pro typy tokenů a barvy pro obsah XML, který se zobrazí v prostředí Windows PowerShell ISE. Token barev můžete nastavit pro následující: Atribut, příkaz, CommandArgument, CommandParameter, komentáře, GroupEnd, GroupStart, – klíčové slovo, LineContinuation, LoopLabel, člen, nový řádek, číslo, – operátor, pozice, StatementSeparator, řetězec, typ, neznámý, proměnné. Viz také [RestoreDefaultXmlTokenColors](#restoredefaultxmltokencolors).

```powershell
# Sets the color of XML element names to green.
$psISE.Options.XmlTokenColors["ElementName"] = 'green'
# Sets the color of XML comments to magenta.
$psISE.Options.XmlTokenColors["Comment"] = 'magenta'
```

### <a name="zoom"></a>Přiblížení

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Určuje relativní velikost textu v konzole i skript podoken. Výchozí hodnota je 100. Menší hodnoty způsobit, že text v prostředí Windows PowerShell ISE zobrazit menší, zatímco velký způsobit větší textu. Hodnota je celé číslo od 20 do 400.

```powershell
# Changes the text in the Windows PowerShell ISE to be double its normal size.
$psISE.Options.Zoom = 200
```

## <a name="see-also"></a>Viz také

- [Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)