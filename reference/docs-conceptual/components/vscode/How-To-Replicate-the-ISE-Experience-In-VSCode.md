---
title: Jak replikovat prostředí ISE v aplikaci Visual Studio Code
description: Jak replikovat prostředí ISE v aplikaci Visual Studio Code
ms.date: 08/06/2018
ms.openlocfilehash: 983da850c13d72bcdc7b2d33970c6e9e06b3d869
ms.sourcegitcommit: 9df29dfc637191b62ca591893c251c1e02d4eb4c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54012479"
---
# <a name="how-to-replicate-the-ise-experience-in-visual-studio-code"></a>Jak replikovat prostředí ISE v aplikaci Visual Studio Code

Když rozšíření prostředí PowerShell pro VSCode nepodporuje hledání paritu funkcí kompletní pomocí prostředí PowerShell ISE, jsou na místě, aby prostředí VSCode přirozenější pro uživatele ISE funkce.

Tento dokument se pokusí o nastavení seznamu, která můžete konfigurovat ve VSCode, aby se uživateli víc známý ve srovnání s ISE.

## <a name="key-bindings"></a>Klávesové zkratky

| Funkce                              | Vazba ISE                  | Vazba VSCode                              |
| ----------------                      | -----------                  | --------------                              |
| Přerušení a přerušení ladicího programu          | <kbd>CTRL</kbd>+<kbd>B</kbd> | <kbd>F6</kbd>                               |
| Spustit aktuální řádek nebo zvýrazněný text | <kbd>F8</kbd>                | <kbd>F8</kbd>                               |
| Seznam dostupných fragmentů               | <kbd>CTRL</kbd>+<kbd>J</kbd> | <kbd>CTRL</kbd>+<kbd>Alt</kbd>+<kbd>J</kbd> |

### <a name="custom-key-bindings"></a>Vlastních vazeb klíče

Je možné [nakonfigurovat vlastní klávesové zkratky](https://code.visualstudio.com/docs/getstarted/keybindings#_custom-keybindings-for-refactorings) ve VSCode také.

## <a name="tab-completion"></a>Dokončování pomocí tabulátoru

Pokud chcete povolit více ISE jako dokončování pomocí tabulátoru, přidejte toto nastavení:

```json
"editor.tabCompletion": "on"
```

> [!NOTE]
> Toto nastavení bylo přidáno přímo do VSCode (spíše než v rozšíření). Její chování je určeno VSCode přímo a nedá se změnit rozšíření.

## <a name="no-focus-on-console-when-executing"></a>Žádné se zaměřují na konzole při provádění

Zachovat fokus v editoru při spouštění s <kbd>F8</kbd>:

```json
"powershell.integratedConsole.focusConsoleOnExecute": false
```

Výchozí hodnota je `true` v zájmu usnadnění přístupu.

## <a name="dont-start-integrated-console-on-startup"></a>Integrovaná konzola nezačínají na spuštění

Pokud chcete zastavit integrovaná konzola při spuštění, nastavte:

```json
"powershell.integratedConsole.showOnStartup": false
```

> [!NOTE]
> Prostředí PowerShell proces na pozadí se spustí stále od, která poskytuje technologii IntelliSense, skript analýzy, navigaci pomocí symbolů, atd. Ale konzole se nezobrazí.

## <a name="assume-files-are-powershell-by-default"></a>Předpokládejme, že soubory jsou ve výchozím nastavení prostředí PowerShell

Chcete-li nový/bez názvu souborů, zaregistrujte se ve výchozím nastavení jako prostředí PowerShell:

```json
"files.defaultLanguage": "powershell"
```

## <a name="color-scheme"></a>Barevné schéma

Nejsou k dispozici pro VSCode aby editor vypadat mnohem více jako ISE počet ISE motivů.

V [Paleta příkazů] typ `theme` zobrazíte `Preferences: Color Theme` a stiskněte klávesu <kbd>Enter</kbd>.
V rozevíracím seznamu vyberte `PowerShell ISE`.

Tento motiv můžete nastavit v nastavení pomocí:

```json
"workbench.colorTheme": "PowerShell ISE"
```

## <a name="powershell-command-explorer"></a>Průzkumník příkaz prostředí PowerShell

Díky práci [ @corbob ](https://github.com/corbob), rozšíření prostředí PowerShell má začátku své vlastní příkaz explorer.

V [Paleta příkazů], zadejte `PowerShell Command Explorer` a stiskněte klávesu <kbd>Enter</kbd>.

## <a name="open-in-the-ise"></a>Otevřít v prostředí ISE

Když ale nakonec se chce k otevření souboru v prostředí ISE i přesto, můžete použít <kbd>Shift</kbd>+<kbd>Alt</kbd>+<kbd>P</kbd>.

## <a name="other-resources"></a>Další prostředky

- má 4sysops [skvělý článek](https://4sysops.com/archives/make-visual-studio-code-look-and-behave-like-powershell-ise/) týkající se konfigurace VSCode bude spíše ISE.
- Mike F Robbins má [skvělý příspěvek](https://mikefrobbins.com/2017/08/24/how-to-install-visual-studio-code-and-configure-it-as-a-replacement-for-the-powershell-ise/) o nastavení VSCode.
- Zjištění Powershellu [vynikající zápisu nahoru](https://www.learnpwsh.com/setup-vs-code-for-powershell/) na získání VSCode nastavení pro prostředí PowerShell.

## <a name="more-settings"></a>Další nastavení

Pokud víte o další způsoby, jak VSCode ISE uživatelé obeznámeni, přispívat do tohoto dokumentu. Pokud není kompatibilita konfigurace, kterou hledáte, ale nemůžete najít žádný způsob, jak povolit, [otevřete problém](https://github.com/PowerShell/vscode-powershell/issues/new/choose) a zeptejte!

Rádi vždy tak, aby přijímal žádosti o přijetí změn a také do nich přispívat.

## <a name="vscode-tips"></a>Tipy pro VSCode

### <a name="command-palette"></a>Paleta příkazů

<kbd>F1</kbd> nebo <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> (<kbd>Cmd</kbd> + <kbd> Posunout</kbd>+<kbd>P</kbd> v systému macOS)

Praktický způsob spouštění příkazů ve VSCode.
Další informace najdete v tématu [dokumentace VSCode](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette).

[Paleta příkazů]: #command-palette
