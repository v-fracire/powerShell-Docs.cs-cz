---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Psání a spouštění skriptů v prostředí Windows PowerShell ISE
ms.assetid: 62f916d9-b3a1-484a-bdfb-41f57112c22b
ms.openlocfilehash: 4d7c5352ef1dac6f63a50433676068f83a920db5
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/07/2018
ms.locfileid: "34483113"
---
# <a name="how-to-write-and-run-scripts-in-the-windows-powershell-ise"></a>Psání a spouštění skriptů v prostředí Windows PowerShell ISE

Toto téma popisuje, jak vytvořit, upravit, spuštění a uložit skripty v podokně skriptu.

## <a name="how-to-create-and-run-scripts"></a>Postup vytvoření a spouštět skripty.

Můžete otevírat a upravovat soubory prostředí Windows PowerShell v podokně skriptu. Určité typy souborů zájmu v prostředí Windows PowerShell jsou soubory skriptu (.ps1), skript datových souborů (.psd1) a soubory modulu skriptu (.psm1). Tyto typy souborů jsou syntaxe barevné v editoru panelu Skript. Další běžné typy souborů, které může zobrazit v podokně skriptu jsou konfigurační soubory (.ps1xml), soubory XML a textové soubory.

> [!NOTE]
> Zásady spouštění prostředí Windows PowerShell Určuje, zda můžete spouštět skripty a zatížení profily prostředí Windows PowerShell a konfigurační soubory. Výchozí zásady spouštění, brání spuštění všech skriptů s omezeným přístupem a zabrání načítání profily. Chcete-li změnit zásady spouštění umožňující profily se načíst a použít, najdete v části [Set-ExecutionPolicy [PSITPro5_Security]](https://technet.microsoft.com/library/5690a0e1-495b-4e63-8280-65ead7bf01ab) a [about_Signing [v4]](https://technet.microsoft.com/library/fcbdd3b9-0b9f-4734-b5c7-e0dcc304fa1d).

### <a name="to-create-a-new-script-file"></a>Chcete-li vytvořit nový soubor skriptu

Na panelu nástrojů klikněte na tlačítko **nový** , nebo na **soubor** nabídky, klikněte na tlačítko **nový**. Vytvořený soubor se zobrazí na nové záložce souboru na kartě aktuální prostředí PowerShell. Mějte na paměti, že prostředí PowerShell karty jsou viditelné pouze když je více než jeden. Ve výchozím nastavení se vytvoří soubor skriptu typ (.ps1), ale nelze uložit s novým názvem a rozšíření. Více souborů skriptu lze vytvořit na stejné kartě prostředí PowerShell.

### <a name="to-open-an-existing-script"></a>Chcete-li otevřít existující skript

Na panelu nástrojů klikněte na tlačítko **otevřete**, nebo na **soubor** nabídky, klikněte na tlačítko **otevřete**. V **otevřete** dialogové okno, vyberte soubor, který chcete otevřít. Otevřený soubor se zobrazí na nové kartě.

### <a name="to-close-a-script-tab"></a>Zavřete kartu skript

Klikněte na kartu skriptu skriptu, který chcete zavřít, a poté proveďte jednu z následujících akcí:

1. Klikněte **Zavřít** ikona (X) na kartě skriptu.

2. Na **soubor** nabídky, klikněte na tlačítko **Zavřít**.

Pokud soubor byla změněna od posledního uložení, zobrazí se výzva k uložte nebo zahoďte ho.

### <a name="to-display-the-file-path"></a>Chcete-li zobrazit cestu k souboru

Na kartě Soubor přejděte na název souboru. Úplná cesta k souboru skriptu se zobrazí ve formě popisu tlačítka.

### <a name="to-run-a-script"></a>Spuštění skriptu

Na panelu nástrojů klikněte na tlačítko **spustit skript**, nebo na **soubor** nabídky, klikněte na tlačítko **spustit**.

### <a name="to-run-a-portion-of-a-script"></a>Ke spuštění část skriptu

1. V podokně skriptu vyberte část skriptu.

2. Na **soubor** nabídky, klikněte na tlačítko **spustit výběr**, nebo na panelu nástrojů klikněte na tlačítko **spustit výběr**.

### <a name="to-stop-a-running-script"></a>Zastavit spuštěné skriptu

Na panelu nástrojů klikněte na tlačítko **zastavit operaci**, stiskněte kombinaci kláves CTRL + BREAK, nebo na **soubor** nabídky, klikněte na tlačítko **zastavit operaci**. Stisknutím **CTRL + C** funguje taky Pokud některé je aktuálně vybraný text, v takovém případě **CTRL + C** se mapuje na funkci kopírování pro vybraný text.

## <a name="how-to-write-and-edit-text-in-the-script-pane"></a>Postup zápisu a upravit text v podokně skriptu

Pomocí následujících kroků lze upravit text v podokně skriptu. Můžete zkopírovat, Vyjmout, vložte, najít a nahradit text. Můžete také vrátit zpět a znovu provést poslední akci, kterou jste právě provedli. Klávesové zkratky pro provádění tyto akce jsou stejné jako pro všechny aplikace systému Windows.

### <a name="to-enter-text-in-the-script-pane"></a>Zadání textu v podokně skriptu

1. Přesunutí kurzoru do podokna skriptu, klepnutím na libovolné místo v podokně skriptu, nebo klikněte na **přejděte do podokna skriptu** v **zobrazení** nabídky.

2. Vytvořte skript. Barevné zvýrazňování syntaxe a dokončování pomocí tabulátorů vytvořit bohatší možnosti v systému Windows PowerShell ISE.

3. V tématu [postup dokončování pomocí tabulátorů použijte v skriptu podokně a podokně konzoly](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) podrobnosti o použití funkci doplňování karta při zadání.

### <a name="to-find-text-in-the-script-pane"></a>Najít text v podokně skriptu

1. Chcete-li najít text kdekoli, stiskněte **CTRL + F** nebo na **upravit** nabídky, klikněte na tlačítko **najít ve skriptu**.

2. Chcete-li najít text po kurzor, stiskněte **F3** nebo na **upravit** nabídky, klikněte na tlačítko **najít další ve skriptu**.

3. Chcete-li najít text před kurzor, stiskněte **SHIFT + F3** nebo na **upravit** nabídky, klikněte na tlačítko **najít předchozí ve skriptu**.

### <a name="to-find-and-replace-text-in-the-script-pane"></a>K vyhledání a nahrazení textu v podokně skriptu

Stiskněte klávesu **CTRL + H** nebo na **upravit** nabídky, klikněte na tlačítko **nahradit ve skriptu**. Zadejte text, který chcete najít a text, pro který chcete nahradit, a potom stiskněte klávesu **ENTER**.

### <a name="to-go-to-a-particular-line-of-text-in-the-script-pane"></a>Přejít na konkrétní řádku textu v podokně skriptu

1. V podokně skriptu stiskněte **kombinaci kláves CTRL + G** nebo na **upravit** nabídky, klikněte na tlačítko **přechod na řádek**.

2. Zadejte číslo řádku.

### <a name="to-copy-text-in-the-script-pane"></a>Zkopírujte text v podokně skriptu

1. V podokně skriptu vyberte text, který chcete zkopírovat.

2. Stiskněte klávesu **CTRL + C** nebo na panelu nástrojů klikněte na tlačítko **kopie** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **kopie**.

### <a name="to-cut-text-in-the-script-pane"></a>Vyjímání text v podokně skriptu

1. V podokně skriptu vyberte text, který chcete vyjmout.

2. Stiskněte klávesu **CTRL + X** nebo na panelu nástrojů klikněte na tlačítko **Vyjmout** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **Vyjmout**.

### <a name="to-paste-text-into-the-script-pane"></a>Chcete vložit text do podokna skriptu

Stiskněte klávesu **CTRL + V** nebo na panelu nástrojů klikněte na tlačítko **vložení** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **vložení**.

### <a name="to-undo-an-action-in-the-script-pane"></a>Postup vrácení akce v podokně skriptu

Stiskněte klávesu **CTRL + Z** nebo na panelu nástrojů klikněte na tlačítko **vrátit zpět** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **vrátit zpět**.

### <a name="to-redo-an-action-in-the-script-pane"></a>Opakování akce v podokně skriptu

Stiskněte klávesu **CTRL + Y** nebo na panelu nástrojů klikněte na tlačítko **vrátit** ikonu, nebo na **upravit** nabídky, klikněte na tlačítko **vrátit**.

## <a name="how-to-save-a-script"></a>Jak uložit skriptu

Pomocí následujících kroků pro uložení a název skriptu. Vedle názvu skriptu k označení soubor, který ještě nebyl uložen, protože byla změněna se zobrazuje hvězdička. Hvězdička zmizí při uložení souboru.

### <a name="to-save-a-script"></a>Uložte skript

Stiskněte klávesu **CTRL + S** nebo na panelu nástrojů klikněte na tlačítko **Uložit** ikonu, nebo na **soubor** nabídky, klikněte na tlačítko **Uložit**.

### <a name="to-save-and-name-a-script"></a>Uložte a název skriptu

1. Na **soubor** nabídky, klikněte na tlačítko **uložit jako**. **Uložit jako** se zobrazí dialogové okno.

2. V **název souboru** pole, zadejte název souboru.

3. V **uložit jako typ** , vyberte typ souboru. Například v **uložit jako typ** vyberte ' œPowerShell skripty (\* .ps1)'.

4. Klikněte na **Uložit**.

### <a name="to-save-a-script-in-ascii-encoding"></a>Uložte skript v kódování ASCII

Ve výchozím nastavení Windows PowerShell ISE uloží nové soubory skriptu (.ps1), skript datových souborů (.psd1) a soubory modulu skriptu (.psm1) jako Unicode (BigEndianUnicode) ve výchozím nastavení. Některá k uložení skript v jiné kódování, jako je například ASCII (ANSI), použijte **Uložit** nebo **uložit jako** metody [$psISE.CurrentFile](https://technet.microsoft.com/library/bc3300e4-9c17-4f00-a621-c8867126e3b3#CurrentFile) objektu.

Následující příkaz uloží nový skript jako MyScript.ps1 s kódováním ASCII.

```powershell
$psISE.CurrentFile.SaveAs("MyScript.ps1", [System.Text.Encoding]::ASCII)
```

Následující příkaz nahradí aktuální soubor skriptu soubor se stejným názvem, ale s kódováním ASCII.

```powershell
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)
```

Následující příkaz získá kódování aktuálního souboru.

```powershell
$psISE.CurrentFile.encoding
```

Windows PowerShell ISE podporuje následující možnosti kódování: ASCII, BigEndianUnicode, kódování Unicode, UTF32, UTF7, UTF8 a výchozí. Hodnota výchozí možnost se liší podle systému.

Windows PowerShell ISE nezmění kódování skripty, které byly vytvořené v jiných editory, i když použijete uložit nebo uložit jako příkazů v systému Windows PowerShell ISE.

## <a name="see-also"></a>Viz také

- [Seznámení s prostředím Windows PowerShell ISE](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)