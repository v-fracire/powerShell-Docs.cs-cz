---
ms.date: 08/14/2018
keywords: rutiny prostředí PowerShell
title: Psání a spouštění skriptů v prostředí Windows PowerShell ISE
ms.assetid: 62f916d9-b3a1-484a-bdfb-41f57112c22b
ms.openlocfilehash: 61db5e18f05e8e334cd9ba6dab2cf15dee7390cc
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403736"
---
# <a name="how-to-write-and-run-scripts-in-the-windows-powershell-ise"></a>Psání a spouštění skriptů v prostředí Windows PowerShell ISE

Tento článek popisuje, jak vytvořit, upravit, spustit a uložit skripty v podokně skriptu.

## <a name="how-to-create-and-run-scripts"></a>Jak vytvořit a spustit skripty

Můžete otevřít a upravit soubory prostředí Windows PowerShell v podokně skriptu. Určité typy souborů zájmu v prostředí Windows PowerShell jsou soubory skriptů (.ps1), datové soubory skriptu (.psd1) a soubory modulu skriptu (.psm1). Tyto typy souborů se syntaxe zobrazí v podokně se skriptem editoru. Další běžné typy souborů, které můžete otevřít z podokna skriptu jsou konfigurační soubory (.ps1xml), soubory XML a textové soubory.

> [!NOTE]
> Zásady spouštění prostředí Windows PowerShell Určuje, zda můžete spustit skripty a načíst profily prostředí Windows PowerShell a konfigurační soubory. Výchozí zásadu spouštění, brání spuštění všech skriptů s omezeným přístupem a brání načítání profilů. Chcete-li změnit zásady spouštění povolit profily a načíst a použít, najdete v článku [Set-ExecutionPolicy](/powershell/module/microsoft.powershell.security/set-executionpolicy) a [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing).

### <a name="to-create-a-new-script-file"></a>Chcete-li vytvořit nový soubor skriptu

Na panelu nástrojů klikněte na tlačítko **nový**, nebo **souboru** nabídky, klikněte na tlačítko **nový**. Vytvořený soubor se zobrazí na nové kartě souboru na aktuální kartě prostředí PowerShell. Mějte na paměti, že karty Powershellu se zobrazují pouze když existuje více než jedna. Ve výchozím nastavení se vytvoří soubor typ skriptu (.ps1), ale může být uložen s novým názvem a příponou. Na stejné kartě Powershellu lze vytvořit více souborů skriptu.

### <a name="to-open-an-existing-script"></a>Chcete-li otevřít existující skript

Na panelu nástrojů klikněte na tlačítko **otevřít**, nebo na **souboru** nabídky, klikněte na tlačítko **otevřít**. V **otevřete** dialogového okna, vyberte soubor, který chcete otevřít. Otevřený soubor se zobrazí na nové záložce.

### <a name="to-close-a-script-tab"></a>Zavřete kartu skript

Klikněte na tlačítko **zavřete** ikonu (X) karty souboru, kterou chcete zavřít nebo vyberte **souboru** nabídky a klikněte na tlačítko **zavřete**.

Pokud soubor byl změněn od posledního uložení, budete vyzváni k ukládání nebo zahazování ho.

### <a name="to-display-the-file-path"></a>Chcete-li zobrazit cestu k souboru

Na kartě souborů odkazovat na název souboru. V popisku se zobrazí plně kvalifikovanou cestu k souboru skriptu.

### <a name="to-run-a-script"></a>Spustit skript

Na panelu nástrojů klikněte na tlačítko **spustit skript**, nebo **souboru** nabídky, klikněte na tlačítko **spustit**.

### <a name="to-run-a-portion-of-a-script"></a>Chcete-li spustit část skriptu

1. V podokně skriptu vyberte část skriptu.
2. Na **souboru** nabídky, klikněte na tlačítko **spustit výběr**, nebo na panelu nástrojů klikněte na tlačítko **spustit výběr**.

### <a name="to-stop-a-running-script"></a>Chcete-li zastavit spouštění skriptu

Existuje několik způsobů, jak zastavit spouštění skriptu.

- Klikněte na tlačítko **zastavení operace** na panelu nástrojů
- Stiskněte kombinaci kláves CTRL + BREAK
- Vyberte **souboru** nabídky a klikněte na tlačítko **zastavení operace**.

Stisknutím klávesy **CTRL + C** funguje i pokud některé je aktuálně vybraný text, v takovém případě **CTRL + C** mapuje na funkci kopírování pro vybraný text.

## <a name="how-to-write-and-edit-text-in-the-script-pane"></a>Psání a upravit text z podokna skriptu

Můžete zkopírovat, Vyjmout, vložit, najít a nahradit text v podokně skriptu. Můžete také vrátit zpět a znovu provést poslední akci, kterou jste právě provedli. Klávesové zkratky pro tyto akce jsou stejné klávesové zkratky používá pro všechny aplikace Windows.

### <a name="to-enter-text-in-the-script-pane"></a>Zadání textu z podokna skriptu

1. Přesunutí kurzoru v podokně skriptu kliknutím na libovolné místo v podokně skriptu, nebo kliknutím **přejděte do podokna skriptu** v **zobrazení** nabídky.
2. Vytvořte skript. Barevné zvýrazňování syntaxe a dokončování pomocí tabulátoru poskytnout bohatší možnosti úprav v prostředí Windows PowerShell ISE.
3. Zobrazit [postupy použití Tab k dokončování příkazů ve skriptovacím podokně a podokně konzoly](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) podrobné informace o použití funkce dokončování kartu na pomoc při psaní.

### <a name="to-find-text-in-the-script-pane"></a>Hledání textu v podokně skriptu

1. Chcete-li vyhledat text kdekoli, stiskněte **CTRL + F** nebo na **upravit** nabídky, klikněte na tlačítko **najít ve skriptu**.
2. Hledání v textu od kurzoru, stiskněte klávesu **F3** nebo na **upravit** nabídky, klikněte na tlačítko **najít další ve skriptu**.
3. Hledání v textu před kurzor, stiskněte klávesu **SHIFT + F3** nebo na **upravit** nabídky, klikněte na tlačítko **najít předchozí ve skriptu**.

### <a name="to-find-and-replace-text-in-the-script-pane"></a>Najít a nahradit text z podokna skriptu

Stisknutím klávesy **CTRL + H** nebo na **upravit** nabídky, klikněte na tlačítko **nahraďte ve skriptu**. Zadejte text, který má k hledání a Nahrazovací text, stiskněte klávesu **ENTER**.

### <a name="to-go-to-a-particular-line-of-text-in-the-script-pane"></a>Chcete-li přejít na konkrétní řádek textu z podokna skriptu

1. V podokně skriptu stisknutím klávesy **CTRL + G** nebo na **upravit** nabídky, klikněte na tlačítko **přejít na řádek**.

2. Zadejte číslo řádku.

### <a name="to-copy-text-in-the-script-pane"></a>Zkopírujte text z podokna skriptu

1. V podokně skriptu vyberte text, který chcete zkopírovat.

2. Stisknutím klávesy **CTRL + C** nebo na panelu nástrojů klikněte na tlačítko **kopírování** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **kopírování**.

### <a name="to-cut-text-in-the-script-pane"></a>Vyjmout text z podokna skriptu

1. V podokně skriptu vyberte text, který chcete vyjmout.
2. Stisknutím klávesy **CTRL + X** nebo na panelu nástrojů klikněte na tlačítko **Vyjmout** ikonu, nebo **upravit** nabídky, klikněte na tlačítko **Vyjmout**.

### <a name="to-paste-text-into-the-script-pane"></a>Vložte text do podokno skriptu

Stisknutím klávesy **CTRL + V** nebo na panelu nástrojů klikněte na tlačítko **vložit** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **vložit**.

### <a name="to-undo-an-action-in-the-script-pane"></a>Vrátit zpět akci z podokna skriptu

Stisknutím klávesy **CTRL + Z** nebo na panelu nástrojů klikněte na tlačítko **zpět** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **zpět**.

### <a name="to-redo-an-action-in-the-script-pane"></a>Opakování akce z podokna skriptu

Stisknutím klávesy **CTRL + Y** nebo na panelu nástrojů klikněte na tlačítko **znovu** ikonu, nebo **upravit** nabídky, klikněte na tlačítko **znovu**.

## <a name="how-to-save-a-script"></a>Uložení skriptu

Hvězdičku vedle názvu skriptu k označení souborů, který dosud nebyl uložen, protože se změnil. Hvězdička zmizí při uložení souboru.

### <a name="to-save-a-script"></a>Uložte skript

Stisknutím klávesy **CTRL + S** nebo na panelu nástrojů klikněte na tlačítko **Uložit** ikonu, nebo na **souboru** nabídky, klikněte na tlačítko **Uložit**.

### <a name="to-save-and-name-a-script"></a>Uložte a název skriptu

1. Na **souboru** nabídky, klikněte na tlačítko **uložit jako**. **Uložit jako** se zobrazí dialogové okno.
2. V **název_souboru** pole, zadejte název souboru.
3. V **uložit jako typ** , vyberte typ souboru. Například v **uložit jako typ** vyberte "skriptů Powershellu (\*.ps1)".
4. Klikněte na **Uložit**.

### <a name="to-save-a-script-in-ascii-encoding"></a>Uložte skript v kódování ASCII

Ve výchozím nastavení Windows PowerShell ISE uloží nové soubory skriptu (.ps1), datové soubory skriptu (.psd1) a soubory modulu skriptu (.psm1) jako kódování Unicode (BigEndianUnicode) ve výchozím nastavení. Některá uložit skript v jiné kódování, jako je například ASCII (ANSI), použijte **Uložit** nebo **SaveAs** metody [$psISE.CurrentFile](object-model/the-ise-object-model-hierarchy.md) objektu.

Následující příkaz uloží nový skript jako MyScript.ps1 s kódováním ASCII.

```powershell
$psISE.CurrentFile.SaveAs("MyScript.ps1", [System.Text.Encoding]::ASCII)
```

Následující příkaz nahradí aktuální soubor skriptu se souborem se stejným názvem, ale s kódováním ASCII.

```powershell
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)
```

V následujícím příkazu je získán kódování aktuálního souboru.

```powershell
$psISE.CurrentFile.encoding
```

Windows PowerShell ISE podporuje následující možnosti kódování: ASCII, BigEndianUnicode, Unicode, UTF32, UTF7, UTF8 a výchozí. Hodnotu výchozí možnosti se liší podle systému.

Windows PowerShell ISE nedojde ke změně kódování souborů skriptu, použijete-li uložit nebo uložit jako příkazy.

## <a name="see-also"></a>Viz také

- [Seznámení s prostředím Windows PowerShell ISE](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
