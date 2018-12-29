---
title: Jak replikovat prostředí ISE v aplikaci Visual Studio Code
description: Jak replikovat prostředí ISE v aplikaci Visual Studio Code
ms.date: 08/06/2018
ms.openlocfilehash: 0ac38985a842a0dfc6118d0ae7116d12e1579daf
ms.sourcegitcommit: 548547b2d5fc73e726bb9fec6175d452a351d975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2018
ms.locfileid: "53655502"
---
# <a name="how-to-replicate-the-ise-experience-in-visual-studio-code"></a><span data-ttu-id="12bd9-103">Jak replikovat prostředí ISE v aplikaci Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="12bd9-103">How to replicate the ISE experience in Visual Studio Code</span></span>

<span data-ttu-id="12bd9-104">Když rozšíření prostředí PowerShell pro VSCode nepodporuje hledání paritu funkcí kompletní pomocí prostředí PowerShell ISE, jsou na místě, aby prostředí VSCode přirozenější pro uživatele ISE funkce.</span><span class="sxs-lookup"><span data-stu-id="12bd9-104">While the PowerShell extension for VSCode doesn't seek complete feature parity with the PowerShell ISE, there are features in place to make the VSCode experience more natural for users of the ISE.</span></span>

<span data-ttu-id="12bd9-105">Tento dokument se pokusí o nastavení seznamu, která můžete konfigurovat ve VSCode, aby se uživateli víc známý ve srovnání s ISE.</span><span class="sxs-lookup"><span data-stu-id="12bd9-105">This document tries to list settings you can configure in VSCode to make the user experience a bit more familiar compared to the ISE.</span></span>

## <a name="key-bindings"></a><span data-ttu-id="12bd9-106">Klávesové zkratky</span><span class="sxs-lookup"><span data-stu-id="12bd9-106">Key bindings</span></span>

| <span data-ttu-id="12bd9-107">Funkce</span><span class="sxs-lookup"><span data-stu-id="12bd9-107">Function</span></span>                              | <span data-ttu-id="12bd9-108">Vazba ISE</span><span class="sxs-lookup"><span data-stu-id="12bd9-108">ISE Binding</span></span>                  | <span data-ttu-id="12bd9-109">Vazba VSCode</span><span class="sxs-lookup"><span data-stu-id="12bd9-109">VSCode Binding</span></span>                              |
| ----------------                      | -----------                  | --------------                              |
| <span data-ttu-id="12bd9-110">Přerušení a přerušení ladicího programu</span><span class="sxs-lookup"><span data-stu-id="12bd9-110">Interrupt and break debugger</span></span>          | <span data-ttu-id="12bd9-111"><kbd>CTRL</kbd>+<kbd>B</kbd></span><span class="sxs-lookup"><span data-stu-id="12bd9-111"><kbd>Ctrl</kbd>+<kbd>B</kbd></span></span> | <span data-ttu-id="12bd9-112"><kbd>F6</kbd></span><span class="sxs-lookup"><span data-stu-id="12bd9-112"><kbd>F6</kbd></span></span>                               |
| <span data-ttu-id="12bd9-113">Spustit aktuální řádek nebo zvýrazněný text</span><span class="sxs-lookup"><span data-stu-id="12bd9-113">Execute current line/highlighted text</span></span> | <span data-ttu-id="12bd9-114"><kbd>F8</kbd></span><span class="sxs-lookup"><span data-stu-id="12bd9-114"><kbd>F8</kbd></span></span>                | <span data-ttu-id="12bd9-115"><kbd>F8</kbd></span><span class="sxs-lookup"><span data-stu-id="12bd9-115"><kbd>F8</kbd></span></span>                               |
| <span data-ttu-id="12bd9-116">Seznam dostupných fragmentů</span><span class="sxs-lookup"><span data-stu-id="12bd9-116">List available snippets</span></span>               | <span data-ttu-id="12bd9-117"><kbd>CTRL</kbd>+<kbd>J</kbd></span><span class="sxs-lookup"><span data-stu-id="12bd9-117"><kbd>Ctrl</kbd>+<kbd>J</kbd></span></span> | <span data-ttu-id="12bd9-118"><kbd>CTRL</kbd>+<kbd>Alt</kbd>+<kbd>J</kbd></span><span class="sxs-lookup"><span data-stu-id="12bd9-118"><kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>J</kbd></span></span> |

### <a name="custom-key-bindings"></a><span data-ttu-id="12bd9-119">Vlastních vazeb klíče</span><span class="sxs-lookup"><span data-stu-id="12bd9-119">Custom Key bindings</span></span>

<span data-ttu-id="12bd9-120">Je možné [nakonfigurovat vlastní klávesové zkratky](https://code.visualstudio.com/docs/getstarted/keybindings#_custom-keybindings-for-refactorings) ve VSCode také.</span><span class="sxs-lookup"><span data-stu-id="12bd9-120">You can [configure your own key bindings](https://code.visualstudio.com/docs/getstarted/keybindings#_custom-keybindings-for-refactorings) in VSCode as well.</span></span>

## <a name="tab-completion"></a><span data-ttu-id="12bd9-121">Dokončování pomocí tabulátoru</span><span class="sxs-lookup"><span data-stu-id="12bd9-121">Tab completion</span></span>

<span data-ttu-id="12bd9-122">Pokud chcete povolit více ISE jako dokončování pomocí tabulátoru, přidejte toto nastavení:</span><span class="sxs-lookup"><span data-stu-id="12bd9-122">To enable more ISE-like tab completion, add this setting:</span></span>

```json
"editor.tabCompletion": "on"
```

> [!NOTE]
> <span data-ttu-id="12bd9-123">Toto nastavení bylo přidáno přímo do VSCode (spíše než v rozšíření).</span><span class="sxs-lookup"><span data-stu-id="12bd9-123">This setting was added directly to VSCode (rather than in the extension).</span></span> <span data-ttu-id="12bd9-124">Její chování je určeno VSCode přímo a nedá se změnit rozšíření.</span><span class="sxs-lookup"><span data-stu-id="12bd9-124">Its behavior is determined by VSCode directly and cannot be changed by the extension.</span></span>

## <a name="no-focus-on-console-when-executing"></a><span data-ttu-id="12bd9-125">Žádné se zaměřují na konzole při provádění</span><span class="sxs-lookup"><span data-stu-id="12bd9-125">No focus on console when executing</span></span>

<span data-ttu-id="12bd9-126">Zachovat fokus v editoru při spouštění s <kbd>F8</kbd>:</span><span class="sxs-lookup"><span data-stu-id="12bd9-126">To keep the focus in the editor when you execute with <kbd>F8</kbd>:</span></span>

```json
"powershell.integratedConsole.focusConsoleOnExecute": false
```

<span data-ttu-id="12bd9-127">Výchozí hodnota je `true` v zájmu usnadnění přístupu.</span><span class="sxs-lookup"><span data-stu-id="12bd9-127">The default is `true` for accessibility purposes.</span></span>

## <a name="dont-start-integrated-console-on-startup"></a><span data-ttu-id="12bd9-128">Integrovaná konzola nezačínají na spuštění</span><span class="sxs-lookup"><span data-stu-id="12bd9-128">Don't start integrated console on startup</span></span>

<span data-ttu-id="12bd9-129">Pokud chcete zastavit integrovaná konzola při spuštění, nastavte:</span><span class="sxs-lookup"><span data-stu-id="12bd9-129">To stop the integrated console on startup, set:</span></span>

```json
"powershell.integratedConsole.showOnStartup": false
```

> [!NOTE]
> <span data-ttu-id="12bd9-130">Prostředí PowerShell proces na pozadí se spustí stále od, která poskytuje technologii intellisense, skript analýzy, navigaci pomocí symbolů, atd. Ale konzole se nezobrazí.</span><span class="sxs-lookup"><span data-stu-id="12bd9-130">The background PowerShell process will still start since that provides intellisense, script analysis, symbol navigation, etc. But the console won't be shown.</span></span>

## <a name="assume-files-are-powershell-by-default"></a><span data-ttu-id="12bd9-131">Předpokládejme, že soubory jsou ve výchozím nastavení prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="12bd9-131">Assume files are PowerShell by default</span></span>

<span data-ttu-id="12bd9-132">Chcete-li nový/bez názvu souborů, zaregistrujte se ve výchozím nastavení jako prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="12bd9-132">To make new/untitled files, register as PowerShell by default:</span></span>

```json
"files.defaultLanguage": "powershell"
```

## <a name="color-scheme"></a><span data-ttu-id="12bd9-133">Barevné schéma</span><span class="sxs-lookup"><span data-stu-id="12bd9-133">Color scheme</span></span>

<span data-ttu-id="12bd9-134">Nejsou k dispozici pro VSCode aby editor vypadat mnohem více jako ISE počet ISE motivů.</span><span class="sxs-lookup"><span data-stu-id="12bd9-134">There are a number of ISE themes available for VSCode to make the editor look much more like the ISE.</span></span>

<span data-ttu-id="12bd9-135">V [Paleta příkazů] typ `theme` zobrazíte `Preferences: Color Theme` a stiskněte klávesu <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="12bd9-135">In the [Command Palette] type `theme` to get `Preferences: Color Theme` and press <kbd>Enter</kbd>.</span></span>
<span data-ttu-id="12bd9-136">V rozevíracím seznamu vyberte `PowerShell ISE`.</span><span class="sxs-lookup"><span data-stu-id="12bd9-136">In the drop-down list, select `PowerShell ISE`.</span></span>

<span data-ttu-id="12bd9-137">Tento motiv můžete nastavit v nastavení pomocí:</span><span class="sxs-lookup"><span data-stu-id="12bd9-137">You can set this theme in the settings with:</span></span>

```json
"workbench.colorTheme": "PowerShell ISE"
```

## <a name="powershell-command-explorer"></a><span data-ttu-id="12bd9-138">Průzkumník příkaz prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="12bd9-138">PowerShell Command Explorer</span></span>

<span data-ttu-id="12bd9-139">Díky práci [ @corbob ](https://github.com/corbob), rozšíření prostředí PowerShell má začátku své vlastní příkaz explorer.</span><span class="sxs-lookup"><span data-stu-id="12bd9-139">Thanks to the work of [@corbob](https://github.com/corbob), the PowerShell extension has the beginnings of its own command explorer.</span></span>

<span data-ttu-id="12bd9-140">V [Paleta příkazů], zadejte `PowerShell Command Explorer` a stiskněte klávesu <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="12bd9-140">In the [Command Palette], enter `PowerShell Command Explorer` and press <kbd>Enter</kbd>.</span></span>

## <a name="open-in-the-ise"></a><span data-ttu-id="12bd9-141">Otevřít v prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="12bd9-141">Open in the ISE</span></span>

<span data-ttu-id="12bd9-142">Když ale nakonec se chce k otevření souboru v prostředí ISE i přesto, můžete použít <kbd>Shift</kbd>+<kbd>Alt</kbd>+<kbd>P</kbd>.</span><span class="sxs-lookup"><span data-stu-id="12bd9-142">If you end up wanting to open a file in the ISE anyway, you can use <kbd>Shift</kbd>+<kbd>Alt</kbd>+<kbd>P</kbd>.</span></span>

## <a name="other-resources"></a><span data-ttu-id="12bd9-143">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="12bd9-143">Other resources</span></span>

- <span data-ttu-id="12bd9-144">má 4sysops [skvělý článek](https://4sysops.com/archives/make-visual-studio-code-look-and-behave-like-powershell-ise/) týkající se konfigurace VSCode bude spíše ISE.</span><span class="sxs-lookup"><span data-stu-id="12bd9-144">4sysops has [a great article](https://4sysops.com/archives/make-visual-studio-code-look-and-behave-like-powershell-ise/) on configuring VSCode to be more like the ISE.</span></span>
- <span data-ttu-id="12bd9-145">Mike F Robbins má [skvělý příspěvek](https://mikefrobbins.com/2017/08/24/how-to-install-visual-studio-code-and-configure-it-as-a-replacement-for-the-powershell-ise/) o nastavení VSCode.</span><span class="sxs-lookup"><span data-stu-id="12bd9-145">Mike F Robbins has [a great post](https://mikefrobbins.com/2017/08/24/how-to-install-visual-studio-code-and-configure-it-as-a-replacement-for-the-powershell-ise/) on setting up VSCode.</span></span>
- <span data-ttu-id="12bd9-146">Zjištění Powershellu [vynikající zápisu nahoru](https://www.learnpwsh.com/setup-vs-code-for-powershell/) na získání VSCode nastavení pro prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12bd9-146">Learn PowerShell has [an excellent write up](https://www.learnpwsh.com/setup-vs-code-for-powershell/) on getting VSCode setup for PowerShell.</span></span>

## <a name="more-settings"></a><span data-ttu-id="12bd9-147">Další nastavení</span><span class="sxs-lookup"><span data-stu-id="12bd9-147">More settings</span></span>

<span data-ttu-id="12bd9-148">Pokud víte o další způsoby, jak VSCode ISE uživatelé obeznámeni, přispívat do tohoto dokumentu. Pokud není kompatibilita konfigurace, kterou hledáte, ale nemůžete najít žádný způsob, jak povolit, [otevřete problém](https://github.com/PowerShell/vscode-powershell/issues/new/choose) a zeptejte!</span><span class="sxs-lookup"><span data-stu-id="12bd9-148">If you know of more ways to make VSCode feel more familiar for ISE users, contribute to this doc. If there's a compatibility configuration you're looking for, but you can't find any way to enable it, [open an issue](https://github.com/PowerShell/vscode-powershell/issues/new/choose) and ask away!</span></span>

<span data-ttu-id="12bd9-149">Rádi vždy tak, aby přijímal žádosti o přijetí změn a také do nich přispívat.</span><span class="sxs-lookup"><span data-stu-id="12bd9-149">We're always happy to accept PRs and contributions as well!</span></span>

## <a name="vscode-tips"></a><span data-ttu-id="12bd9-150">Tipy pro VSCode</span><span class="sxs-lookup"><span data-stu-id="12bd9-150">VSCode Tips</span></span>

### <a name="command-palette"></a><span data-ttu-id="12bd9-151">Paleta příkazů</span><span class="sxs-lookup"><span data-stu-id="12bd9-151">Command Palette</span></span>

<span data-ttu-id="12bd9-152"><kbd>F1</kbd> nebo <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> (<kbd>Cmd</kbd> + <kbd> Posunout</kbd>+<kbd>P</kbd> v systému macOS)</span><span class="sxs-lookup"><span data-stu-id="12bd9-152"><kbd>F1</kbd> OR <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> (<kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> on macOS)</span></span>

<span data-ttu-id="12bd9-153">Praktický způsob spouštění příkazů ve VSCode.</span><span class="sxs-lookup"><span data-stu-id="12bd9-153">A handy way of executing commands in VSCode.</span></span>
<span data-ttu-id="12bd9-154">Další informace najdete v tématu [dokumentace VSCode](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette).</span><span class="sxs-lookup"><span data-stu-id="12bd9-154">For more information, see [the VSCode docs](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette).</span></span>

[Paleta příkazů]: #command-palette
[Command Palette]: #command-palette
