---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Seznámení s prostředím Windows PowerShell ISE
ms.assetid: e0d2c6e8-5126-40e7-a1e1-d1cff29fe94a
ms.openlocfilehash: 059651f159fb2636a93167709134788e90d062b8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403865"
---
# <a name="exploring-the-windows-powershell-ise"></a>Seznámení s prostředím Windows PowerShell ISE

Windows PowerShell® integrovaném skriptovacím prostředí (ISE) můžete použít k vytvoření, spuštění a ladění příkazy a skripty. Windows PowerShell ISE se skládá z řádku nabídek, karty prostředí Windows PowerShell, panelu nástrojů, skript karty, podokno skriptu, podokně konzoly, stavového řádku, posuvník velikost textu a kontextové nápovědy.

> [!NOTE]
> Od verze 3.0 ISE Windows Powershellu příkaz a výstupní podokna byly sloučeny do jediného konzoly.

## <a name="menu-bar"></a>Panel nabídek

Panel nabídek obsahuje **souboru**, **upravit**, **zobrazení**, **nástroje**, **ladění**,  **Doplňky**, a **pomáhají** nabídky. Tlačítka v nabídkách umožňují provádět úlohy související s psaní a spuštěných skriptů a spouštění příkazů v prostředí Windows PowerShell ISE. Kromě toho [doplněk Nástroje](../../core-powershell/ise/The-ISEAddOnTool-Object.md) můžete umístit na řádku nabídek díky spouštění skriptů, které používají [The hierarchie objektového modelu prostředí ISE](../../core-powershell/ise/The-ISE-Object-Model-Hierarchy.md).

> [!NOTE]
> Ve Windows PowerShell ISE 2.0 **nástroje** a **doplňky** nabídky nebyly k dispozici.

## <a name="windows-powershell-tabs"></a>Karty Windows Powershellu

Karta prostředí Windows PowerShell je prostředí, ve kterém se spustí skript Windows Powershellu. Nové karty v prostředí Windows PowerShell můžete otevřít v prostředí Windows PowerShell ISE vytvořit samostatná prostředí v místním počítači nebo na vzdálených počítačích. Může mít maximálně osm Powershellu karty najednou otevřít.

## <a name="toolbar"></a>Panel nástrojů

Následující tlačítka jsou umístěny na panelu nástrojů.

|Tlačítko|Funkce|
|----------|------------|
|**Nový**|Otevře se nový skript.|
|**Otevřít**|Otevře existující skriptu nebo soubor.|
|**Uložení**|Uloží skriptu nebo soubor.|
|**Vyjmout**|Vyjme vybraný text a zkopíruje do schránky.|
|**Kopírování**|Zkopíruje vybraný text do schránky.|
|**Vložit**|Vloží obsah schránky do umístění kurzoru.|
|**Vymazat podokno výstup**|Vymaže veškerý obsah v podokně výstup.|
|**Vrácení zpět**|Obrátí akci, která se právě provedla.|
|**Znovu:**|Provede akci, která byla právě vrátit zpět.|
|**Spuštění skriptu**|Spustí skript.|
|**Spustit výběr**|Spustí vybranou část skriptu.|
|**Zastavit provádění**|Zastaví skript, který je spuštěn.|
|**Nová karta vzdáleného prostředí PowerShell**|Vytvoří nová karta prostředí PowerShell, který vytvoří relaci ve vzdáleném počítači. Dialogové okno se zobrazí a zobrazí výzvu k zadání podrobností, které jsou potřebné k navázání vzdáleného připojení.|
|**Spustit PowerShell.exe**|Otevře se konzola Powershellu.|
|**Zobrazit horní podokno skriptu**|V podokně skriptu přesune do horní části v zobrazení.|
|**Zobrazit podokno skriptu vpravo**|Posune podokno skriptu vpravo v zobrazení.|
|**Zobrazit podokno skriptu maximalizované**|Maximalizuje v podokně skriptu.|

## <a name="script-tab"></a>Karta skriptu

Název skriptu, který upravujete. Můžete kliknout na kartu skript vyberte skript, který chcete upravit.

Když přejdete na kartu skript, plně kvalifikovanou cestu k souboru skriptu se zobrazí v popisku.

## <a name="script-pane"></a>Podokno skriptu

Umožňuje vytvářet a spouštět skripty. Můžete otevřít, upravit a spustit stávající skripty v podokně skriptu.

## <a name="output-pane"></a>Podokno výstup

Zobrazí výsledky příkazy a skripty, které jste spustili. Můžete také zkopírovat a vymazat obsah v podokně výstup.

## <a name="command-pane"></a>Příkazového podokna

Umožňuje psát příkazy. Můžete spustit příkaz jeden řádek nebo víceřádkové příkazu v příkazovém podokně. Stiskněte SHIFT + ENTER každý řádek víceřádkové příkaz a stiskněte klávesu ENTER po poslední řádek ke spuštění příkazu víceřádkový. Řádku zobrazit nad v příkazovém podokně zobrazuje cestu k aktuálnímu pracovnímu adresáři.

## <a name="status-bar"></a>Stavový řádek

Umožňuje zobrazit, zda jsou příkazy a skripty, které můžete spouštět kompletní. Stavový řádek je úplně dole v zobrazení. Vybrané části chybové zprávy se zobrazují na stavovém řádku.

## <a name="text-size-slider"></a>Velikost textu posuvníku

Zvětší nebo zmenší velikost textu na obrazovce.

## <a name="help"></a>Nápověda

Nápověda prostředí Windows PowerShell ISE je dostupné na webu v knihovně TechNet. Nápovědy můžete otevřít kliknutím **nápovědu k prostředí Windows PowerShell ISE** na **pomáhají** nabídky nebo stisknutím klávesy F1 kdekoli s výjimkou případů, když je kurzor na název rutiny v podokně skriptu nebo konzole. Z **pomáhají** nabídky můžete taky spustit rutinu Update-Help a zobrazit příkazové okno, které vám pomůže při konstrukci příkazy zobrazující všechny parametry rutiny a povolením můžete vyplnit parametry v Formulář snadným ovládáním.

## <a name="see-also"></a>Viz také

- [Představení Windows PowerShell ISE](../../core-powershell/ise/Introducing-the-Windows-PowerShell-ISE.md)