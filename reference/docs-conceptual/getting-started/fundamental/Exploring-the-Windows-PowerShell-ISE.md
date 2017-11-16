---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Zkoumání Windows PowerShell ISE"
ms.assetid: e0d2c6e8-5126-40e7-a1e1-d1cff29fe94a
ms.openlocfilehash: 979209d4b200728b7e78e341bb9595741d2b8e68
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="exploring-the-windows-powershell-ise"></a>Zkoumání Windows PowerShell ISE
Windows PowerShell® Integrované skriptovací prostředí (ISE) slouží k vytvoření, spuštění a ladění příkazy a skripty. Windows PowerShell ISE se skládá z řádku nabídek, karty prostředí Windows PowerShell, panelu nástrojů, karty skriptu, podokno skriptu, podokna konzoly, stavového řádku, velikost textu posuvníku a kontextová nápověda.

> [!NOTE]
> Od verze prostředí Windows PowerShell ISE 3.0 příkaz a výstupní podokna byly zkombinované do jednoho podokna konzoly.

## <a name="menu-bar"></a>Panel nabídek
Panel nabídek obsahuje **soubor**, **upravit**, **zobrazení**, **nástroje**, **ladění**,  **Doplňky**, a **pomoci** nabídky. Tlačítka v nabídkách umožňují provádět úkoly související se zápisy a spuštěné skripty a příkazy spuštěné v systému Windows PowerShell ISE. Navíc [rozšíření nástroj](../../core-powershell/ise/The-ISEAddOnTool-Object.md) může být umístěna na panelu nabídek pomocí spouštění skriptů, které používají [Windows PowerShell ISE skriptování objektový Model](../../core-powershell/ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md).

> [!NOTE]
> V prostředí Windows PowerShell ISE 2.0 **nástroje** a **doplňky** nabídky nebyly k dispozici.

## <a name="windows-powershell-tabs"></a>Windows PowerShell karty
Na kartě prostředí Windows PowerShell je prostředí, ve kterém se spouští skript prostředí Windows PowerShell. Nové karty prostředí Windows PowerShell můžete otevřít v ISE Windows PowerShell k vytvoření samostatných prostředí v místním počítači nebo na vzdálených počítačích. Můžete mít maximálně osm PowerShell karty současně otevřít.

## <a name="toolbar"></a>Panel nástrojů
Následující tlačítka jsou umístěny na panelu nástrojů.

|Tlačítko|Funkce|
|----------|------------|
|**Nový**|Otevře se nový skript.|
|**Otevřete**|Otevře existující skriptu nebo soubor.|
|**Uložit**|Uloží soubor skriptu nebo soubor.|
|**Vyjmout**|Vyjme vybrané text a zkopíruje jej do schránky.|
|**Kopírování**|Zkopíruje vybraný text do schránky.|
|**Vložení**|Vloží obsah schránky do umístění kurzoru.|
|**Vymazat podokno výstup**|Vymaže veškerý obsah v podokně výstup.|
|**Vrácení zpět**|Obrátí akci, která se právě provádí.|
|**Znovu:**|Provede akci, která vrácenou zpět.|
|**Spuštění skriptu**|Spouští skript.|
|**Spustit Selction**|Spustí vybranou část skriptu.|
|**Zastavit provádění**|Zastaví skript, který běží.|
|**Novou kartu vzdáleného prostředí PowerShell**|Vytvoří novou kartu prostředí PowerShell, který vytvoří relaci ve vzdáleném počítači. Dialogové okno se zobrazí a výzvu k zadání podrobností nutný k vytvoření vzdáleného připojení.|
|**Spustit PowerShell.exe**|Otevře se konzole prostředí PowerShell.|
|**Zobrazit nejlepší podokně skriptu**|V podokně skriptu přesune do horní části v zobrazení.|
|**Zobrazit podokno skriptu vpravo**|V podokně skriptu přesune vpravo v zobrazení.|
|**Zobrazit podokno skriptu maximalizovaný**|Maximalizuje podokně skriptu.|

## <a name="script-tab"></a>Karta skriptu
Zobrazí název skriptu, který upravujete. Můžete kliknout na kartu skript skriptů, které chcete upravit.

Přejděte na kartu skriptu, zobrazí se v popisek plně kvalifikovanou cestu k souboru skriptu.

## <a name="script-pane"></a>Podokno skriptu
Umožňuje vytvářet a spouštět skripty. Můžete otevřít, upravit a spustit existující skripty v podokně skriptu.

## <a name="output-pane"></a>V podokně výstupu
Zobrazí výsledky příkazy a skripty, které jste spustili. Můžete také zkopírovat a vymazat obsah v podokně výstup.

## <a name="command-pane"></a>Příkaz Podokno
Umožňuje psát příkazy. V podokně příkaz můžete spustit příkaz jeden řádek nebo víceřádkových příkazu. Stiskněte SHIFT + ENTER zadejte každého řádku Víceřádkový příkaz a stiskněte klávesu ENTER za posledním řádkem Víceřádkový příkazů. Řádku zobrazit nad podokně příkaz zobrazuje cestu k aktuální pracovní adresář.

## <a name="status-bar"></a>Stavový řádek
Umožňuje zobrazit, zda jsou příkazy a skripty, které spustíte dokončení. Stavový řádek je velmi dole v zobrazení. Vybrané části chybové zprávy se zobrazují na stavovém řádku.

## <a name="text-size-slider"></a>Velikost textu posuvníku
Zvyšuje nebo snižuje velikost textu na obrazovce.

## <a name="help"></a>Nápověda
Nápověda pro prostředí Windows PowerShell ISE je k dispozici na webu v knihovně TechNet. V nápovědě můžete otevřít kliknutím **nápovědy prostředí Windows PowerShell ISE** na **pomoci** nabídky nebo po stisknutí klávesy F1 kdekoli kromě případů, kdy kurzor na název rutiny, v podokně skriptu nebo podokně konzoly. Z **pomoci** nabídky můžete taky spustit rutinu Update-Help a zobrazit příkazové okno, který slouží k vytváření příkazů ukazuje všechny parametry rutiny a povolením k vyplnění v parametrech v Snadné použití formulář.

## <a name="see-also"></a>Viz také
- [Pomocí Windows PowerShell ISE](../../core-powershell/ise/Using-the-Windows-PowerShell-ISE.md)

