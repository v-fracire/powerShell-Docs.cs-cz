---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEOptions
ms.assetid: 75e2a76f-f3d1-490b-ad5d-e3829946aabb
ms.openlocfilehash: e756da21aaa5465f7fa6a90563b4180f0c89e87b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953646"
---
# <a name="the-iseoptions-object"></a><span data-ttu-id="edf15-103">Objekt ISEOptions</span><span class="sxs-lookup"><span data-stu-id="edf15-103">The ISEOptions Object</span></span>

<span data-ttu-id="edf15-104">**ISEOptions** objekt představuje různá nastavení pro Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="edf15-104">The **ISEOptions** object represents various settings for Windows PowerShell ISE.</span></span> <span data-ttu-id="edf15-105">Je instance **Microsoft.PowerShell.Host.ISE.ISEOptions** třídy.</span><span class="sxs-lookup"><span data-stu-id="edf15-105">It is an instance of the **Microsoft.PowerShell.Host.ISE.ISEOptions** class.</span></span>

<span data-ttu-id="edf15-106">**ISEOptions** objekt poskytuje následující metody a vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="edf15-106">The **ISEOptions** object provides the following methods and properties.</span></span>

## <a name="methods"></a><span data-ttu-id="edf15-107">Metody</span><span class="sxs-lookup"><span data-stu-id="edf15-107">Methods</span></span>

### <a name="restoredefaultconsoletokencolors"></a><span data-ttu-id="edf15-108">RestoreDefaultConsoleTokenColors\(\)</span><span class="sxs-lookup"><span data-stu-id="edf15-108">RestoreDefaultConsoleTokenColors\(\)</span></span>

<span data-ttu-id="edf15-109">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-109">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-110">Obnoví výchozí hodnoty tokenu barvy v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-110">Restores the default values of the token colors in the Console pane.</span></span>

```powershell
# Changes the color of the commands in the Console pane to red and then restores it to its default value.
$psISE.Options.ConsoleTokenColors["Command"] = 'red'
$psISE.Options.RestoreDefaultConsoleTokenColors()
```

### <a name="restoredefaults"></a><span data-ttu-id="edf15-111">RestoreDefaults\(\)</span><span class="sxs-lookup"><span data-stu-id="edf15-111">RestoreDefaults\(\)</span></span>

<span data-ttu-id="edf15-112">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-112">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-113">Obnoví výchozí hodnoty nastavení možností v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-113">Restores the default values of all options settings in the Console pane.</span></span> <span data-ttu-id="edf15-114">Obnoví také chování různých zprávy upozornění, které poskytují standardní zaškrtnutím políčka zabránit se znovu zobrazí zpráva.</span><span class="sxs-lookup"><span data-stu-id="edf15-114">It also resets the behavior of various warning messages that provide the standard check box to prevent the message from being shown again.</span></span>

```powershell
# Changes the background color in the Console pane and then restores it to its default value.
$psISE.Options.ConsolePaneBackgroundColor = 'orange'
$psISE.Options.RestoreDefaults()
```

### <a name="restoredefaulttokencolors"></a><span data-ttu-id="edf15-115">RestoreDefaultTokenColors\(\)</span><span class="sxs-lookup"><span data-stu-id="edf15-115">RestoreDefaultTokenColors\(\)</span></span>

<span data-ttu-id="edf15-116">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-116">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-117">Obnoví výchozí hodnoty tokenu barvy v podokně skriptu.</span><span class="sxs-lookup"><span data-stu-id="edf15-117">Restores the default values of the token colors in the Script pane.</span></span>

```powershell
# Changes the color of the comments in the Script pane to red and then restores it to its default value.
$psISE.Options.TokenColors["Comment"] = 'red'
$psISE.Options.RestoreDefaultTokenColors()
```

### <a name="restoredefaultxmltokencolors"></a><span data-ttu-id="edf15-118">RestoreDefaultXmlTokenColors\(\)</span><span class="sxs-lookup"><span data-stu-id="edf15-118">RestoreDefaultXmlTokenColors\(\)</span></span>

<span data-ttu-id="edf15-119">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-119">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-120">Obnoví výchozí hodnoty tokenu barvy pro elementy XML, které se zobrazují v systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="edf15-120">Restores the default values of the token colors for XML elements that are displayed in Windows PowerShell ISE.</span></span> <span data-ttu-id="edf15-121">Viz také [XmlTokenColors](#xmltokencolors).</span><span class="sxs-lookup"><span data-stu-id="edf15-121">Also see [XmlTokenColors](#xmltokencolors).</span></span>

```powershell
# Changes the color of the comments in XML data to red and then restores it to its default value.
$psISE.Options.XmlTokenColors["Comment"] = 'red'
$psISE.Options.RestoreDefaultXmlTokenColors()
```

## <a name="properties"></a><span data-ttu-id="edf15-122">Properties</span><span class="sxs-lookup"><span data-stu-id="edf15-122">Properties</span></span>

### <a name="autosaveminuteinterval"></a><span data-ttu-id="edf15-123">AutoSaveMinuteInterval</span><span class="sxs-lookup"><span data-stu-id="edf15-123">AutoSaveMinuteInterval</span></span>

<span data-ttu-id="edf15-124">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-124">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-125">Určuje počet minut mezi operacemi automatického ukládání souborů pomocí Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="edf15-125">Specifies the number of minutes between automatic save operations of your files by Windows PowerShell ISE.</span></span> <span data-ttu-id="edf15-126">Výchozí hodnota je 2 minut.</span><span class="sxs-lookup"><span data-stu-id="edf15-126">The default value is 2 minutes.</span></span> <span data-ttu-id="edf15-127">Hodnota je celé číslo.</span><span class="sxs-lookup"><span data-stu-id="edf15-127">The value is an integer.</span></span>

```powershell
# Changes the number of minutes between automatic save operations to every 3 minutes.
$psISE.Options.AutoSaveMinuteInterval = 3
```

### <a name="commandpanebackgroundcolor"></a><span data-ttu-id="edf15-128">CommandPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-128">CommandPaneBackgroundColor</span></span>

<span data-ttu-id="edf15-129">Tato funkce je k dispozici v prostředí Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.</span><span class="sxs-lookup"><span data-stu-id="edf15-129">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="edf15-130">Novější verze najdete v tématu [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).</span><span class="sxs-lookup"><span data-stu-id="edf15-130">For later versions, see [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).</span></span>

<span data-ttu-id="edf15-131">Určuje barvu pozadí pro příkaz podokně.</span><span class="sxs-lookup"><span data-stu-id="edf15-131">Specifies the background color for the Command pane.</span></span> <span data-ttu-id="edf15-132">Je instance **System.Windows.Media.Color** třídy.</span><span class="sxs-lookup"><span data-stu-id="edf15-132">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Changes the background color of the Command pane to orange.
$psISE.Options.CommandPaneBackgroundColor = 'orange'
```

### <a name="commandpaneup"></a><span data-ttu-id="edf15-133">CommandPaneUp</span><span class="sxs-lookup"><span data-stu-id="edf15-133">CommandPaneUp</span></span>

<span data-ttu-id="edf15-134">Tato funkce je k dispozici v prostředí Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.</span><span class="sxs-lookup"><span data-stu-id="edf15-134">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>

<span data-ttu-id="edf15-135">Určuje, zda se nachází v podokně příkaz výše podokno výstup.</span><span class="sxs-lookup"><span data-stu-id="edf15-135">Specifies whether the Command pane is located above the Output pane.</span></span>

```powershell
# Moves the Command pane to the top of the screen.
$psISE.Options.CommandPaneUp  = $true
```

### <a name="consolepanebackgroundcolor"></a><span data-ttu-id="edf15-136">ConsolePaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-136">ConsolePaneBackgroundColor</span></span>

<span data-ttu-id="edf15-137">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-137">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-138">Určuje barvu pozadí panelu konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-138">Specifies the background color for the Console pane.</span></span> <span data-ttu-id="edf15-139">Je instance **System.Windows.Media.Color** třídy.</span><span class="sxs-lookup"><span data-stu-id="edf15-139">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Changes the background color of the Console pane to red.
$psISE.Options.ConsolePaneBackgroundColor = 'red'
```

### <a name="consolepaneforegroundcolor"></a><span data-ttu-id="edf15-140">ConsolePaneForegroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-140">ConsolePaneForegroundColor</span></span>

<span data-ttu-id="edf15-141">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-141">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-142">Určuje barvu popředí textu v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-142">Specifies the foreground color of the text in the Console pane.</span></span>

```powershell
# Changes the foreground color of the text in the Console pane to yellow.
$psISE.Options.ConsolePaneForegroundColor  = 'yellow'
```

### <a name="consolepanetextbackgroundcolor"></a><span data-ttu-id="edf15-143">ConsolePaneTextBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-143">ConsolePaneTextBackgroundColor</span></span>

<span data-ttu-id="edf15-144">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-144">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-145">Určuje barvu pozadí textu v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-145">Specifies the background color of the text in the Console pane.</span></span>

```powershell
# Changes the background color of the Console pane text to pink.
$psISE.Options.ConsolePaneTextBackgroundColor = 'pink'
```

### <a name="consoletokencolors"></a><span data-ttu-id="edf15-146">ConsoleTokenColors</span><span class="sxs-lookup"><span data-stu-id="edf15-146">ConsoleTokenColors</span></span>

<span data-ttu-id="edf15-147">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-147">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-148">Určuje barvy tokenů IntelliSense v podokně konzoly ISE Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="edf15-148">Specifies the colors of the IntelliSense tokens in the Windows PowerShell ISE Console pane.</span></span> <span data-ttu-id="edf15-149">Tato vlastnost je objekt slovník, který obsahuje dvojice název/hodnota pro typy tokenů a barvy pro podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-149">This property is a dictionary object that contains name/value pairs of token types and colors for the Console pane.</span></span> <span data-ttu-id="edf15-150">Chcete-li změnit barvy tokenů IntelliSense v podokně skriptu, [TokenColors](#tokencolors).</span><span class="sxs-lookup"><span data-stu-id="edf15-150">To change the colors of the IntelliSense tokens in the Script pane, see [TokenColors](#tokencolors).</span></span> <span data-ttu-id="edf15-151">Barvy resetovat na výchozí hodnoty, najdete v části [RestoreDefaultConsoleTokenColors](#restoredefaultconsoletokencolors).</span><span class="sxs-lookup"><span data-stu-id="edf15-151">To reset the colors to the default values, see [RestoreDefaultConsoleTokenColors](#restoredefaultconsoletokencolors).</span></span> <span data-ttu-id="edf15-152">Token barvy lze nastavit pro následující: atribut, příkazu, CommandArgument, CommandParameter, komentáře, GroupEnd, GroupStart, – klíčové slovo, LineContinuation, LoopLabel, člen, nový řádek, číslo, operátor, pozice, StatementSeparator, řetězec, typ, Neznámá, proměnné.</span><span class="sxs-lookup"><span data-stu-id="edf15-152">Token colors can be set for the following: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span></span>

```powershell
# Sets the color of commands to green.
$psISE.Options.ConsoleTokenColors["Command"] = 'green'
# Sets the color of keywords to magenta.
$psISE.Options.ConsoleTokenColors["Keyword"] = 'magenta'
```

### <a name="debugbackgroundcolor"></a><span data-ttu-id="edf15-153">DebugBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-153">DebugBackgroundColor</span></span>

<span data-ttu-id="edf15-154">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-154">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-155">Určuje barvu pozadí pro ladění text, který se zobrazí v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-155">Specifies the background color for the debug text that appears in the Console pane.</span></span> <span data-ttu-id="edf15-156">Je instance **System.Windows.Media.Color** třídy.</span><span class="sxs-lookup"><span data-stu-id="edf15-156">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Changes the background color for the debug text that appears in the Console pane to blue.
$psISE.Options.DebugBackgroundColor = '#0000FF'
```

### <a name="debugforegroundcolor"></a><span data-ttu-id="edf15-157">DebugForegroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-157">DebugForegroundColor</span></span>

<span data-ttu-id="edf15-158">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-158">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-159">Určuje barvu popředí pro ladění text, který se zobrazí v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-159">Specifies the foreground color for the debug text that appears in the Console pane.</span></span> <span data-ttu-id="edf15-160">Je instance **System.Windows.Media.Color** třídy.</span><span class="sxs-lookup"><span data-stu-id="edf15-160">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Changes the foreground color for the debug text that appears in the Console pane to yellow.
$psISE.Options.DebugForegroundColor = 'yellow'
```

### <a name="defaultoptions"></a><span data-ttu-id="edf15-161">DefaultOptions</span><span class="sxs-lookup"><span data-stu-id="edf15-161">DefaultOptions</span></span>

<span data-ttu-id="edf15-162">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-162">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-163">Kolekce vlastností, které určují, které se používají při resetování metody se používají výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="edf15-163">A collection of properties that specify the default values to be used when the Reset methods are used.</span></span>

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

### <a name="errorbackgroundcolor"></a><span data-ttu-id="edf15-164">ErrorBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-164">ErrorBackgroundColor</span></span>

<span data-ttu-id="edf15-165">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-165">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-166">Určuje barvu pozadí pro text chyby, který se zobrazí v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-166">Specifies the background color for error text that appears in the Console pane.</span></span> <span data-ttu-id="edf15-167">Je instance **System.Windows.Media.Color** třídy.</span><span class="sxs-lookup"><span data-stu-id="edf15-167">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Changes the background color for the error text that appears in the Console pane to black.
$psISE.Options.ErrorBackgroundColor = 'black'
```

### <a name="errorforegroundcolor"></a><span data-ttu-id="edf15-168">ErrorForegroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-168">ErrorForegroundColor</span></span>

<span data-ttu-id="edf15-169">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-169">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-170">Určuje barvu popředí pro text chyby, který se zobrazí v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-170">Specifies the foreground color for error text that appears in the Console pane.</span></span> <span data-ttu-id="edf15-171">Je instance **System.Windows.Media.Color** třídy.</span><span class="sxs-lookup"><span data-stu-id="edf15-171">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Changes the foreground color for the error text that appears in the console pane to green.
$psISE.Options.ErrorForegroundColor = 'green'
```

### <a name="fontname"></a><span data-ttu-id="edf15-172">FontName</span><span class="sxs-lookup"><span data-stu-id="edf15-172">FontName</span></span>

<span data-ttu-id="edf15-173">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-173">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-174">Určuje název písma aktuálně používá v podokně skriptu a v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-174">Specifies the font name currently in use in both the Script pane and the Console pane.</span></span>

```powershell
# Changes the font used in both panes.
$psISE.Options.FontName = 'Courier New'
```

### <a name="fontsize"></a><span data-ttu-id="edf15-175">Velikost písma</span><span class="sxs-lookup"><span data-stu-id="edf15-175">FontSize</span></span>

<span data-ttu-id="edf15-176">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-176">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-177">Určuje velikost písma jako celé číslo.</span><span class="sxs-lookup"><span data-stu-id="edf15-177">Specifies the font size as an integer.</span></span> <span data-ttu-id="edf15-178">Používá se v podokně skriptu, příkaz podokně a podokně výstup.</span><span class="sxs-lookup"><span data-stu-id="edf15-178">It is used in the Script pane, the Command pane, and the Output pane.</span></span> <span data-ttu-id="edf15-179">Platný rozsah hodnot je 8 až 32.</span><span class="sxs-lookup"><span data-stu-id="edf15-179">The valid range of values is 8 through 32.</span></span>

```powershell
# Changes the font size in all panes.
$psISE.Options.FontSize = 20
```

### <a name="intellisensetimeoutinseconds"></a><span data-ttu-id="edf15-180">IntellisenseTimeoutInSeconds</span><span class="sxs-lookup"><span data-stu-id="edf15-180">IntellisenseTimeoutInSeconds</span></span>

<span data-ttu-id="edf15-181">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-181">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-182">Určuje počet sekund, po které IntelliSense používá k řešení aktuálně zadaný text.</span><span class="sxs-lookup"><span data-stu-id="edf15-182">Specifies the number of seconds that IntelliSense uses to try to resolve the currently typed text.</span></span> <span data-ttu-id="edf15-183">Po tomto počtu sekund IntelliSense vyprší časový limit a umožňuje pokračujte v zadávání.</span><span class="sxs-lookup"><span data-stu-id="edf15-183">After this number of seconds, IntelliSense times out and enables you to continue typing.</span></span> <span data-ttu-id="edf15-184">Výchozí hodnota je 3 sekund.</span><span class="sxs-lookup"><span data-stu-id="edf15-184">The default value is 3 seconds.</span></span> <span data-ttu-id="edf15-185">Hodnota je celé číslo.</span><span class="sxs-lookup"><span data-stu-id="edf15-185">The value is an integer.</span></span>

```powershell
# Changes the number of seconds for IntelliSense syntax recognition to 5.
$psISE.Options.IntellisenseTimeoutInSeconds = 5
```

### <a name="mrucount"></a><span data-ttu-id="edf15-186">MruCount</span><span class="sxs-lookup"><span data-stu-id="edf15-186">MruCount</span></span>

<span data-ttu-id="edf15-187">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-187">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-188">Určuje počet posledních otevřených souborů, které Windows PowerShell ISE sleduje a zobrazí se v dolní části **otevřít soubor** nabídky.</span><span class="sxs-lookup"><span data-stu-id="edf15-188">Specifies the number of recently opened files that Windows PowerShell ISE tracks and displays at the bottom of the **File Open** menu.</span></span> <span data-ttu-id="edf15-189">Výchozí hodnota je 10.</span><span class="sxs-lookup"><span data-stu-id="edf15-189">The default value is 10.</span></span> <span data-ttu-id="edf15-190">Hodnota je celé číslo.</span><span class="sxs-lookup"><span data-stu-id="edf15-190">The value is an integer.</span></span>

```powershell
# Changes the number of recently used files that appear at the bottom of the File Open menu to 5.
$psISE.Options.MruCount = 5
```

### <a name="outputpanebackgroundcolor"></a><span data-ttu-id="edf15-191">OutputPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-191">OutputPaneBackgroundColor</span></span>

<span data-ttu-id="edf15-192">Tato funkce je k dispozici v prostředí Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.</span><span class="sxs-lookup"><span data-stu-id="edf15-192">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="edf15-193">Novější verze najdete v tématu [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).</span><span class="sxs-lookup"><span data-stu-id="edf15-193">For later versions, see [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).</span></span>

<span data-ttu-id="edf15-194">Vlastnost pro čtení a zápis, získá nebo nastaví barvu pozadí pro podokno výstup sám sebe.</span><span class="sxs-lookup"><span data-stu-id="edf15-194">The read/write property that gets or sets the background color for the Output pane itself.</span></span> <span data-ttu-id="edf15-195">Je instance **System.Windows.Media.Color** třídy.</span><span class="sxs-lookup"><span data-stu-id="edf15-195">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Changes the background color of the Output pane to gold.
$psISE.Options.OutputPaneForegroundColor = 'gold'
```

### <a name="outputpanetextforegroundcolor"></a><span data-ttu-id="edf15-196">OutputPaneTextForegroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-196">OutputPaneTextForegroundColor</span></span>

<span data-ttu-id="edf15-197">Tato funkce je k dispozici v prostředí Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.</span><span class="sxs-lookup"><span data-stu-id="edf15-197">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="edf15-198">Novější verze najdete v tématu [ConsolePaneForegroundColor](#consolepaneforegroundcolor).</span><span class="sxs-lookup"><span data-stu-id="edf15-198">For later versions, see [ConsolePaneForegroundColor](#consolepaneforegroundcolor).</span></span>

<span data-ttu-id="edf15-199">Vlastnost pro čtení a zápis, který změní barvu popředí textu v podokně výstup v prostředí Windows PowerShell ISE 2.0.</span><span class="sxs-lookup"><span data-stu-id="edf15-199">The read/write property that changes the foreground color of the text in the Output pane in Windows PowerShell ISE 2.0.</span></span>

```powershell
# Changes the foreground color of the text in the Output Pane to blue.
$psISE.Options.OutputPaneTextForegroundColor  = 'blue'
```

### <a name="outputpanetextbackgroundcolor"></a><span data-ttu-id="edf15-200">OutputPaneTextBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-200">OutputPaneTextBackgroundColor</span></span>

<span data-ttu-id="edf15-201">Tato funkce je k dispozici v prostředí Windows PowerShell ISE 2.0, ale byla odebrat nebo přejmenovat v novějších verzích ISE.</span><span class="sxs-lookup"><span data-stu-id="edf15-201">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="edf15-202">Novější verze najdete v tématu [ConsolePaneTextBackgroundColor](#consolepanetextbackgroundcolor).</span><span class="sxs-lookup"><span data-stu-id="edf15-202">For later versions, see [ConsolePaneTextBackgroundColor](#consolepanetextbackgroundcolor).</span></span>

<span data-ttu-id="edf15-203">Vlastnost pro čtení a zápis, která změní barvu pozadí textu v podokně výstup.</span><span class="sxs-lookup"><span data-stu-id="edf15-203">The read/write property that changes the background color of the text in the Output pane.</span></span>

```powershell
# Changes the background color of the Output pane text to pink.
$psISE.Options.OutputPaneTextBackgroundColor = 'pink'
```

### <a name="scriptpanebackgroundcolor"></a><span data-ttu-id="edf15-204">ScriptPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-204">ScriptPaneBackgroundColor</span></span>

<span data-ttu-id="edf15-205">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-205">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-206">Vlastnost pro čtení a zápis, který získá nebo nastaví barvu pozadí pro soubory.</span><span class="sxs-lookup"><span data-stu-id="edf15-206">The read/write property that gets or sets the background color for files.</span></span> <span data-ttu-id="edf15-207">Je instance **System.Windows.Media.Color** třídy.</span><span class="sxs-lookup"><span data-stu-id="edf15-207">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Sets the color of the script pane background to yellow.
$psISE.Options.ScriptPaneBackgroundColor = 'yellow'
```

### <a name="scriptpaneforegroundcolor"></a><span data-ttu-id="edf15-208">ScriptPaneForegroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-208">ScriptPaneForegroundColor</span></span>

<span data-ttu-id="edf15-209">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-209">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-210">Vlastnost pro čtení a zápis, který získá nebo nastaví barvu popředí pro soubory bez skriptu v podokně skriptu.</span><span class="sxs-lookup"><span data-stu-id="edf15-210">The read/write property that gets or sets the foreground color for non-script files in the Script pane.</span></span>
<span data-ttu-id="edf15-211">Pokud chcete nastavit barvu popředí pro soubory skriptu, použijte [TokenColors](#tokencolors).</span><span class="sxs-lookup"><span data-stu-id="edf15-211">To set the foreground color for script files, use the [TokenColors](#tokencolors).</span></span>

```powershell
# Sets the foreground to color of non-script files in the script pane to green.
$psISE.Options.ScriptPaneBackgroundColor = 'green'
```

### <a name="selectedscriptpanestate"></a><span data-ttu-id="edf15-212">SelectedScriptPaneState</span><span class="sxs-lookup"><span data-stu-id="edf15-212">SelectedScriptPaneState</span></span>

<span data-ttu-id="edf15-213">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-213">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-214">Vlastnost pro čtení a zápis, získá nebo nastaví pozici v podokně skriptu na zobrazení.</span><span class="sxs-lookup"><span data-stu-id="edf15-214">The read/write property that gets or sets the position of the Script pane on the display.</span></span> <span data-ttu-id="edf15-215">Může být řetězec 'Maximized', 'Top' nebo 'Right'.</span><span class="sxs-lookup"><span data-stu-id="edf15-215">The string can be either 'Maximized', 'Top', or 'Right'.</span></span>

```powershell
# Moves the Script Pane to the top.
$psISE.Options.SelectedScriptPaneState = 'Top'
# Moves the Script Pane to the right.
$psISE.Options.SelectedScriptPaneState = 'Right'
# Maximizes the Script Pane
$psISE.Options.SelectedScriptPaneState = 'Maximized'
```

### <a name="showdefaultsnippets"></a><span data-ttu-id="edf15-216">ShowDefaultSnippets</span><span class="sxs-lookup"><span data-stu-id="edf15-216">ShowDefaultSnippets</span></span>

<span data-ttu-id="edf15-217">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-217">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-218">Určuje, zda **CTRL + J** seznam fragmenty obsahuje sadu starter, který je součástí prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="edf15-218">Specifies whether the **CTRL+J** list of snippets includes the starter set that is included in Windows PowerShell.</span></span> <span data-ttu-id="edf15-219">Pokud nastavíte hodnotu **$false**, se zobrazí pouze fragmenty uživatelem definované v **CTRL + J** seznamu.</span><span class="sxs-lookup"><span data-stu-id="edf15-219">When set to **$false**, only user-defined snippets appear in the **CTRL+J** list.</span></span> <span data-ttu-id="edf15-220">Výchozí hodnota je **$true**.</span><span class="sxs-lookup"><span data-stu-id="edf15-220">The default value is **$true**.</span></span>

```powershell
# Hide the default snippets from the CTRL+J list.
$psISE.Options.ShowDefaultSnippets = $false
```

### <a name="showintellisenseinconsolepane"></a><span data-ttu-id="edf15-221">ShowIntellisenseInConsolePane</span><span class="sxs-lookup"><span data-stu-id="edf15-221">ShowIntellisenseInConsolePane</span></span>

<span data-ttu-id="edf15-222">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-222">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-223">Určuje, zda IntelliSense nabízí syntaxi parametru a hodnota návrhy v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-223">Specifies whether IntelliSense offers syntax, parameter, and value suggestions in the Console pane.</span></span> <span data-ttu-id="edf15-224">Výchozí hodnota je **$true**.</span><span class="sxs-lookup"><span data-stu-id="edf15-224">The default value is **$true**.</span></span>

```powershell
# Turn off IntelliSense in the console pane.
$psISE.Options.ShowIntellisenseInConsolePane = $false
```

### <a name="showintellisenseinscriptpane"></a><span data-ttu-id="edf15-225">ShowIntellisenseInScriptPane</span><span class="sxs-lookup"><span data-stu-id="edf15-225">ShowIntellisenseInScriptPane</span></span>

<span data-ttu-id="edf15-226">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-226">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-227">Určuje, zda IntelliSense nabízí syntaxi parametru a hodnota návrhy v podokně skriptu.</span><span class="sxs-lookup"><span data-stu-id="edf15-227">Specifies whether IntelliSense offers syntax, parameter, and value suggestions in the Script pane.</span></span> <span data-ttu-id="edf15-228">Výchozí hodnota je **$true**.</span><span class="sxs-lookup"><span data-stu-id="edf15-228">The default value is **$true**.</span></span>

```powershell
# Turn off IntelliSense in the Script pane.
$psISE.Options.ShowIntellisenseInScriptPane = $false
```

### <a name="showlinenumbers"></a><span data-ttu-id="edf15-229">ShowLineNumbers</span><span class="sxs-lookup"><span data-stu-id="edf15-229">ShowLineNumbers</span></span>

<span data-ttu-id="edf15-230">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-230">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-231">Určuje, zda v podokně skriptu se zobrazí na levém okraji čísla řádků.</span><span class="sxs-lookup"><span data-stu-id="edf15-231">Specifies whether the Script pane displays line numbers in the left margin.</span></span> <span data-ttu-id="edf15-232">Výchozí hodnota je **$true**.</span><span class="sxs-lookup"><span data-stu-id="edf15-232">The default value is **$true**.</span></span>

```powershell
# Turn off line numbers in the Script pane.
$psISE.Options.ShowLineNumbers = $false
```

### <a name="showoutlining"></a><span data-ttu-id="edf15-233">ShowOutlining</span><span class="sxs-lookup"><span data-stu-id="edf15-233">ShowOutlining</span></span>

<span data-ttu-id="edf15-234">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-234">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-235">Určuje, zda v podokně skriptu se zobrazí na levém okraji rozšíření a sbalitelné závorky vedle sekcí kódu.</span><span class="sxs-lookup"><span data-stu-id="edf15-235">Specifies whether the Script pane displays expandable and collapsible brackets next to sections of code in the left margin.</span></span> <span data-ttu-id="edf15-236">Pokud jsou zobrazeny, můžete kliknout na minus \( - \) ikonami vedle blok textu sbalit, nebo kliknutím na tlačítko plus \( + \) ikonu rozbalte blok textu.</span><span class="sxs-lookup"><span data-stu-id="edf15-236">When they are displayed, you can click the minus \(-\) icons next to a block of text to collapse it or click the plus \(+\) icon to expand a block of text.</span></span> <span data-ttu-id="edf15-237">Výchozí hodnota je **$true**.</span><span class="sxs-lookup"><span data-stu-id="edf15-237">The default value is **$true**.</span></span>

```powershell
# Turn off outlining in the Script pane.
$psISE.Options.ShowOutlining = $false
```

### <a name="showtoolbar"></a><span data-ttu-id="edf15-238">ShowToolBar</span><span class="sxs-lookup"><span data-stu-id="edf15-238">ShowToolBar</span></span>

<span data-ttu-id="edf15-239">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-239">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-240">Určuje, zda se zobrazí panelu nástrojů (ISE) v horní části okna Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="edf15-240">Specifies whether the ISE toolbar appears at the top of the Windows PowerShell ISE window.</span></span> <span data-ttu-id="edf15-241">Výchozí hodnota je **$true**.</span><span class="sxs-lookup"><span data-stu-id="edf15-241">The default value is **$true**.</span></span>

```powershell
# Show the toolbar.
$psISE.Options.ShowToolBar = $true
```

### <a name="showwarningbeforesavingonrun"></a><span data-ttu-id="edf15-242">ShowWarningBeforeSavingOnRun</span><span class="sxs-lookup"><span data-stu-id="edf15-242">ShowWarningBeforeSavingOnRun</span></span>

<span data-ttu-id="edf15-243">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-243">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-244">Určuje, zda zpráva upozornění se zobrazí, když skriptu se automaticky uloží, než je spuštěn.</span><span class="sxs-lookup"><span data-stu-id="edf15-244">Specifies whether a warning message appears when a script is saved automatically before it is run.</span></span> <span data-ttu-id="edf15-245">Výchozí hodnota je **$true**.</span><span class="sxs-lookup"><span data-stu-id="edf15-245">The default value is **$true**.</span></span>

```powershell
# Enable the warning message when an attempt
# is made to run a script without saving it first.
$psISE.Options.ShowWarningBeforeSavingOnRun = $true
```

### <a name="showwarningforduplicatefiles"></a><span data-ttu-id="edf15-246">ShowWarningForDuplicateFiles</span><span class="sxs-lookup"><span data-stu-id="edf15-246">ShowWarningForDuplicateFiles</span></span>

<span data-ttu-id="edf15-247">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-247">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-248">Určuje, zda zpráva upozornění se zobrazí, když je stejný soubor otevřít na různých záložkách prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="edf15-248">Specifies whether a warning message appears when the same file is opened in different PowerShell tabs.</span></span> <span data-ttu-id="edf15-249">Pokud nastavena na **$true**, stejný soubor otevřete v několika karty zobrazí tato zpráva: "kopii tohoto souboru je otevřen v jiné kartě prostředí Windows PowerShell. Změny provedené v tomto souboru bude mít vliv na všechny otevřené kopie."</span><span class="sxs-lookup"><span data-stu-id="edf15-249">If set to **$true**, to open the same file in multiple tabs displays this message: "A copy of this file is open in another Windows PowerShell tab. Changes made to this file will affect all open copies."</span></span> <span data-ttu-id="edf15-250">Výchozí hodnota je **$true**.</span><span class="sxs-lookup"><span data-stu-id="edf15-250">The default value is **$true**.</span></span>

```powershell
# Enable the warning message when a file is
# opened in multiple PowerShell tabs.
$psISE.Options.ShowWarningForDuplicateFiles = $true
```

### <a name="tokencolors"></a><span data-ttu-id="edf15-251">TokenColors</span><span class="sxs-lookup"><span data-stu-id="edf15-251">TokenColors</span></span>

<span data-ttu-id="edf15-252">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-252">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-253">Určuje barvy tokenů IntelliSense v podokně skript prostředí Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="edf15-253">Specifies the colors of the IntelliSense tokens in the Windows PowerShell ISE Script pane.</span></span> <span data-ttu-id="edf15-254">Tato vlastnost je objekt slovník, který obsahuje dvojice název/hodnota pro typy tokenů a barvy pro podokně skriptu.</span><span class="sxs-lookup"><span data-stu-id="edf15-254">This property is a dictionary object that contains name/value pairs of token types and colors for the Script pane.</span></span> <span data-ttu-id="edf15-255">Chcete-li změnit barvy tokenů IntelliSense v podokně konzoly, [ConsoleTokenColors](#consoletokencolors).</span><span class="sxs-lookup"><span data-stu-id="edf15-255">To change the colors of the IntelliSense tokens in the Console pane, see [ConsoleTokenColors](#consoletokencolors).</span></span> <span data-ttu-id="edf15-256">Barvy resetovat na výchozí hodnoty, najdete v části [RestoreDefaultTokenColors](#restoredefaulttokencolors).</span><span class="sxs-lookup"><span data-stu-id="edf15-256">To reset the colors to the default values, see [RestoreDefaultTokenColors](#restoredefaulttokencolors).</span></span> <span data-ttu-id="edf15-257">Token barvy lze nastavit pro následující: atribut, příkazu, CommandArgument, CommandParameter, komentáře, GroupEnd, GroupStart, – klíčové slovo, LineContinuation, LoopLabel, člen, nový řádek, číslo, operátor, pozice, StatementSeparator, řetězec, typ, Neznámá, proměnné.</span><span class="sxs-lookup"><span data-stu-id="edf15-257">Token colors can be set for the following: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span></span>

```powershell
# Sets the color of commands to green.
$psISE.Options.TokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.TokenColors["Keyword"] = "magenta"
```

### <a name="useentertoselectinconsolepaneintellisense"></a><span data-ttu-id="edf15-258">UseEnterToSelectInConsolePaneIntellisense</span><span class="sxs-lookup"><span data-stu-id="edf15-258">UseEnterToSelectInConsolePaneIntellisense</span></span>

<span data-ttu-id="edf15-259">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-259">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-260">Určuje, zda můžete použít klávesu Enter a vyberte IntelliSense poskytuje možnost v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-260">Specifies whether you can use the Enter key to select an IntelliSense provided option in the Console pane.</span></span> <span data-ttu-id="edf15-261">Výchozí hodnota je **$true**.</span><span class="sxs-lookup"><span data-stu-id="edf15-261">The default value is **$true**.</span></span>

```powershell
# Turn off using the ENTER key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense = $false
```

### <a name="useentertoselectinscriptpaneintellisense"></a><span data-ttu-id="edf15-262">UseEnterToSelectInScriptPaneIntellisense</span><span class="sxs-lookup"><span data-stu-id="edf15-262">UseEnterToSelectInScriptPaneIntellisense</span></span>

<span data-ttu-id="edf15-263">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-263">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-264">Určuje, zda můžete použít klávesu Enter a vyberte možnost zadaný IntelliSense v podokně skriptu.</span><span class="sxs-lookup"><span data-stu-id="edf15-264">Specifies whether you can use the Enter key to select an IntelliSense-provided option in the Script pane.</span></span> <span data-ttu-id="edf15-265">Výchozí hodnota je **$true**.</span><span class="sxs-lookup"><span data-stu-id="edf15-265">The default value is **$true**.</span></span>

```powershell
# Turn on using the Enter key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense = $true
```

### <a name="uselocalhelp"></a><span data-ttu-id="edf15-266">UseLocalHelp</span><span class="sxs-lookup"><span data-stu-id="edf15-266">UseLocalHelp</span></span>

<span data-ttu-id="edf15-267">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-267">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-268">Určuje, zda lokálně nainstalované nápovědy nebo online knihovně TechNet nápovědy se zobrazí po stisknutí klávesy F1 umístěte kurzor v klíčové slovo.</span><span class="sxs-lookup"><span data-stu-id="edf15-268">Specifies whether the locally installed Help or the online TechNet Library Help appears when you press F1 with the cursor positioned in a keyword.</span></span> <span data-ttu-id="edf15-269">Pokud nastavena na **$true**, pak automaticky otevírané okno zobrazuje obsahu pomocí lokálně nainstalované nápovědy.</span><span class="sxs-lookup"><span data-stu-id="edf15-269">If set to **$true**, then a pop-up window shows content from the locally installed Help.</span></span> <span data-ttu-id="edf15-270">Soubory nápovědy můžete nainstalovat spuštěním `Update-Help` příkaz.</span><span class="sxs-lookup"><span data-stu-id="edf15-270">You can install the Help files by running the `Update-Help` command.</span></span> <span data-ttu-id="edf15-271">Pokud nastavena na **$false**, pak otevře prohlížeč na stránku v knihovně TechNet.</span><span class="sxs-lookup"><span data-stu-id="edf15-271">If set to **$false**, then your browser opens to a page in the TechNet Library.</span></span>

```powershell
# Sets the option for the online help to be displayed.
$psISE.Options.UseLocalHelp = $false
# Sets the option for the local Help to be displayed.
$psISE.Options.UseLocalHelp = $true
```

### <a name="verbosebackgroundcolor"></a><span data-ttu-id="edf15-272">VerboseBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-272">VerboseBackgroundColor</span></span>

<span data-ttu-id="edf15-273">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-273">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-274">Určuje barvu pozadí pro podrobné text, který se zobrazí v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-274">Specifies the background color for verbose text that appears in the Console pane.</span></span> <span data-ttu-id="edf15-275">Je **System.Windows.Media.Color** objektu.</span><span class="sxs-lookup"><span data-stu-id="edf15-275">It is a **System.Windows.Media.Color** object.</span></span>

```powershell
# Changes the background color for verbose text to blue.
$psISE.Options.VerboseBackgroundColor ='#0000FF'
```

### <a name="verboseforegroundcolor"></a><span data-ttu-id="edf15-276">VerboseForegroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-276">VerboseForegroundColor</span></span>

<span data-ttu-id="edf15-277">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-277">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-278">Určuje barvu popředí pro podrobné text, který se zobrazí v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-278">Specifies the foreground color for verbose text that appears in the Console pane.</span></span> <span data-ttu-id="edf15-279">Je **System.Windows.Media.Color** objektu.</span><span class="sxs-lookup"><span data-stu-id="edf15-279">It is a **System.Windows.Media.Color** object.</span></span>

```powershell
# Changes the foreground color for verbose text to yellow.
$psISE.Options.VerboseForegroundColor = 'yellow'
```

### <a name="warningbackgroundcolor"></a><span data-ttu-id="edf15-280">WarningBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-280">WarningBackgroundColor</span></span>

<span data-ttu-id="edf15-281">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-281">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-282">Určuje barvu pozadí pro upozornění text, který se zobrazí v podokně konzoly.</span><span class="sxs-lookup"><span data-stu-id="edf15-282">Specifies the background color for warning text that appears in the Console pane.</span></span> <span data-ttu-id="edf15-283">Je **System.Windows.Media.Color** objektu.</span><span class="sxs-lookup"><span data-stu-id="edf15-283">It is a **System.Windows.Media.Color** object.</span></span>

```powershell
# Changes the background color for warning text to blue.
$psISE.Options.WarningBackgroundColor = '#0000FF'
```

### <a name="warningforegroundcolor"></a><span data-ttu-id="edf15-284">WarningForegroundColor</span><span class="sxs-lookup"><span data-stu-id="edf15-284">WarningForegroundColor</span></span>

<span data-ttu-id="edf15-285">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="edf15-285">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="edf15-286">Určuje barvu popředí pro upozornění text, který se zobrazí v podokně výstup.</span><span class="sxs-lookup"><span data-stu-id="edf15-286">Specifies the foreground color for warning text that appears in the Output pane.</span></span> <span data-ttu-id="edf15-287">Je **System.Windows.Media.Color** objektu.</span><span class="sxs-lookup"><span data-stu-id="edf15-287">It is a **System.Windows.Media.Color** object.</span></span>

```powershell
# Changes the foreground color for warning text to yellow.
$psISE.Options.WarningForegroundColor = 'yellow'
```

### <a name="xmltokencolors"></a><span data-ttu-id="edf15-288">XmlTokenColors</span><span class="sxs-lookup"><span data-stu-id="edf15-288">XmlTokenColors</span></span>

<span data-ttu-id="edf15-289">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-289">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-290">Určuje objekt slovník, který obsahuje dvojice název/hodnota pro typy tokenů a barvy pro obsah XML, který se zobrazí v systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="edf15-290">Specifies a dictionary object that contains name/value pairs of token types and colors for XML content that is displayed in Windows PowerShell ISE.</span></span> <span data-ttu-id="edf15-291">Token barvy lze nastavit pro následující: atribut, příkazu, CommandArgument, CommandParameter, komentáře, GroupEnd, GroupStart, – klíčové slovo, LineContinuation, LoopLabel, člen, nový řádek, číslo, operátor, pozice, StatementSeparator, řetězec, typ, Neznámá, proměnné.</span><span class="sxs-lookup"><span data-stu-id="edf15-291">Token colors can be set for the following: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span></span> <span data-ttu-id="edf15-292">Viz také [RestoreDefaultXmlTokenColors](#restoredefaultxmltokencolors).</span><span class="sxs-lookup"><span data-stu-id="edf15-292">Also see [RestoreDefaultXmlTokenColors](#restoredefaultxmltokencolors).</span></span>

```powershell
# Sets the color of XML element names to green.
$psISE.Options.XmlTokenColors["ElementName"] = 'green'
# Sets the color of XML comments to magenta.
$psISE.Options.XmlTokenColors["Comment"] = 'magenta'
```

### <a name="zoom"></a><span data-ttu-id="edf15-293">Přiblížení</span><span class="sxs-lookup"><span data-stu-id="edf15-293">Zoom</span></span>

<span data-ttu-id="edf15-294">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="edf15-294">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="edf15-295">Určuje relativní velikost textu v konzole i skriptu podokna.</span><span class="sxs-lookup"><span data-stu-id="edf15-295">Specifies the relative size of text in both the Console and Script panes.</span></span> <span data-ttu-id="edf15-296">Výchozí hodnota je 100.</span><span class="sxs-lookup"><span data-stu-id="edf15-296">The default value is 100.</span></span> <span data-ttu-id="edf15-297">Menší hodnoty způsobit, že text v systému Windows PowerShell ISE zobrazí menší při větší počty způsobit text, který se zobrazí větší.</span><span class="sxs-lookup"><span data-stu-id="edf15-297">Smaller values cause the text in Windows PowerShell ISE to appear smaller while larger numbers cause text to appear larger.</span></span> <span data-ttu-id="edf15-298">Hodnota je celé číslo, které se pohybuje od 20 do 400.</span><span class="sxs-lookup"><span data-stu-id="edf15-298">The value is an integer that ranges from 20 to 400.</span></span>

```powershell
# Changes the text in the Windows PowerShell ISE to be double its normal size.
$psISE.Options.Zoom = 200
```

## <a name="see-also"></a><span data-ttu-id="edf15-299">Viz také</span><span class="sxs-lookup"><span data-stu-id="edf15-299">See Also</span></span>

- [<span data-ttu-id="edf15-300">Účelem ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="edf15-300">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="edf15-301">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="edf15-301">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)