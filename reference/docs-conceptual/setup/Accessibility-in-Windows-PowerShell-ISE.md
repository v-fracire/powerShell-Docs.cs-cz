---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Usnadnění přístupu v systému Windows PowerShell ISE"
ms.assetid: a078f9d1-dd6b-4323-b16d-0622cd993aa8
ms.openlocfilehash: 505ec3aca84b5ad0b9d58a1ec84d80e3aa86db7a
ms.sourcegitcommit: 3720ce4efb6735694cfb53a1b793d949af5d1bc5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2017
---
# <a name="accessibility-in-windows-powershell-ise"></a>Usnadnění přístupu v systému Windows PowerShell ISE
Toto téma popisuje funkce usnadnění systému Windows PowerShell Integrované skriptovací prostředí (ISE), mohou být užitečné.

* [Postup změny velikosti a umístění konzoly a podokna skriptu](#how-to-change-the-size-and-location-of-the-console-and-script-panes)
* [Klávesové zkratky pro úpravy textu](#keyboard-shortcuts-for-editing-text)
* [Klávesové zkratky pro spouštění skriptů](#keyboard-shortcuts-for-running-scripts)
* [Klávesové zkratky pro přizpůsobení zobrazení](#keyboard-shortcuts-for-customizing-the-view)
* [Klávesové zkratky pro ladění skriptů](#keyboard-shortcuts-for-debugging-scripts)
* [Klávesové zkratky pro prostředí Windows PowerShell karty](#keyboard-shortcuts-for-windows-powershell-tabs)
* [Klávesové zkratky pro spuštění a ukončení](#keyboard-shortcuts-for-starting-and-exiting)

Společnost Microsoft se zavázala k tomu, aby vytvářela produkty a služby, jejichž používání je snadné pro každého. Následující témata obsahují informace o funkcích, produktech a službách, díky kterým Windows PowerShell ISE přístupnější pro osoby s postižením.

Windows PowerShell ISE podporuje režimu vysokého kontrastu. Pro slabozraké zarážek informace jsou k dispozici prostřednictvím rutin pro správu zarážky, jako například [Get-PSBreakpoint](https://technet.microsoft.com/en-us/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) a [Set-PSBreakpoint](https://technet.microsoft.com/en-us/library/6afd5d2c-a285-4796-8607-3cbf49471420). Další informace najdete v tématu 'Postup správy zarážky' v [postup ladění skriptů v systému Windows PowerShell ISE](../core-powershell/ise/How-to-Debug-Scripts-in-Windows-PowerShell-ISE.md). Kromě funkcí a nástrojů usnadnění v systému Windows následující funkce společnost Windows PowerShell ISE přizpůsobila pro postižené osoby:

- Klávesové zkratky

- Barvy v tabulky syntax a možnost upravit několik dalších nastavení barev pomocí [$psISE.Options](https://technet.microsoft.com/en-us/library/75e2a76f-f3d1-490b-ad5d-e3829946aabb) objekt skriptování.

- Změna velikosti textu

## <a name="how-to-change-the-size-and-location-of-the-console-and-script-panes"></a>Postup změny velikosti a umístění konzoly a podokna skriptu
Chcete-li změnit velikost a umístění v podokně konzole a v podokně skriptu můžete použít následující kroky. Když znovu otevřete Windows PowerShell ISE se uchovají provedené změny velikosti a umístění.

### <a name="to-resize-the-script-pane-and-console-pane"></a>Chcete-li změnit velikost skriptu podokně a podokně konzoly

1. Ukazatel na řádku rozdělení mezi podokno skriptu a podokna konzoly.

2. Jakmile se ukazatel myši změní na dvojitou šipku, přetáhněte okraj ke změně velikosti podokna.

### <a name="to-move-the-script-pane-and-console-pane"></a>Chcete-li přesunout podokno skriptu a podokna konzoly
Udělejte jednu z těchto věcí:

- Chcete-li v podokně skriptu výše podokně konzoly, stiskněte **CTRL + 1** nebo na panelu nástrojů klikněte na tlačítko **zobrazit horní podokno skriptu** ikonu, nebo v **zobrazení** nabídky, klikněte na tlačítko **zobrazit Horní podokno skriptu**.

- Chcete-li v podokně skriptu napravo od panelu konzoly, stiskněte **CTRL + 2** nebo na panelu nástrojů klikněte na tlačítko **zobrazit pravé podokno skriptu** ikonu, nebo v **zobrazení** nabídky, klikněte na tlačítko **Zobrazit podokno skriptu správné**.

- Pokud chcete maximalizovat podokna skriptu, stiskněte **CTRL + 3** nebo na panelu nástrojů klikněte na tlačítko **zobrazit maximalizovaný podokně skriptu** ikonu, nebo v **zobrazení** nabídky, klikněte na tlačítko **zobrazit skript Podokno maximalizovaný**.

- Pokud chcete maximalizovat podokně konzoly a skrýt podokno skriptu na daleko pravý okraj řádku karet, klikněte na tlačítko **skrýt podokno skriptu** ikona v **zobrazení** nabídky, klikněte na tlačítko zrušte výběr **zobrazit podokno skriptu** možnost nabídky.

- Chcete-li zobrazit podokno skriptu maximalizaci podokně konzoly v daleko pravý okraj řádku karet, klikněte na tlačítko **zobrazit podokno skriptu** ikonu, nebo v **zobrazení** nabídky, zaškrtněte **zobrazit skript Podokno** možnost nabídky.

## <a name="keyboard-shortcuts-for-editing-text"></a>Klávesové zkratky pro úpravy textu
Při úpravách text můžete použít následující klávesové zkratky.

|Akce|Klávesové zkratky|Použití v|
|----------|----------------------|----------|
|**Kopírování**|Ctrl + C|Skript nebo podokno konzoly|
|**Vyjmout**|CTRL + X|Skript nebo podokno konzoly|
|**Najít ve skriptu**|CTRL+F|Podokno skriptu|
|**Najít další ve skriptu**|F3|Podokno skriptu|
|**Najít předchozí ve skriptu**|SHIFT + F3|Podokno skriptu|
|**Vložení**|CTRL + V|Skript nebo podokno konzoly|
|**Znovu:**|CTRL + Y|Skript nebo podokno konzoly|
|**Nahraďte ve skriptu**|CTRL + H|Podokno skriptu|
|**Uložit**|CTRL+S|Podokno skriptu|
|**Vybrat vše**|CTRL + A|Skript nebo podokno konzoly|
|**Vrácení zpět**|CTRL + Z|Skript nebo podokno konzoly|

## <a name="keyboard-shortcuts-for-running-scripts"></a>Klávesové zkratky pro spouštění skriptů
Při spouštění skriptů v podokně skriptu můžete použít následující klávesové zkratky.

|Akce|Klávesové zkratky|
|----------|---------------------|
|**Nový**|CTRL + N|
|**Otevřete**|CTRL + O|
|**Spustit**|F5|
|**Spustit výběr**|F8|
|**Zastavit provádění**|CTRL + BREAK. CTRL + C lze použít, pokud kontext je jednoznačné (když není vybrán žádný text).|
|**Karta** (pro další skript)|CTRL + TAB **Poznámka:** a další skript funguje pouze v případě, že máte do jedné karty prostředí PowerShell otevřít, nebo pokud máte více než jedné karty prostředí PowerShell, otevřete, ale zaměřuje se v podokně skriptu.|
|**Karta** (na předchozím skriptu)|CTRL + SHIFT + TAB **Poznámka:** kartě předchozí skriptu funguje, když máte jenom jeden otevřete kartu prostředí PowerShell, nebo pokud máte více než jedné karty prostředí PowerShell otevřít, a v podokně skriptu je aktivní.|

## <a name="keyboard-shortcuts-for-customizing-the-view"></a>Klávesové zkratky pro přizpůsobení zobrazení
Chcete-li přizpůsobit zobrazení v Windows PowerShell ISE můžete použít následující klávesové zkratky. Jsou přístupné ze všech podokna v aplikaci.

|Akce|Klávesové zkratky|
|----------|---------------------|
|**Přejděte do podokna konzoly**|CTRL + D|
|**Přejděte do podokna skriptu**|CTRL + I|
|**Zobrazit podokno skriptu**|CTRL + R|
|**Skrýt podokno skriptu**|CTRL + R|
||
|**Podokno skriptu přesunout nahoru**|CTRL + 1|
|**Pravé podokno skriptu přesunutí**|CTRL + 2|
|**Maximalizovat podokno skriptu**|CTRL + 3|
|**Přiblížení**|CTRL + SYMBOL PLUS|
|**Oddálení**|CTRL + SYMBOL MÍNUS|

## <a name="keyboard-shortcuts-for-debugging-scripts"></a>Klávesové zkratky pro ladění skriptů
Můžete použít následující klávesové zkratky při ladění skriptů.

|Akce|Klávesové zkratky|Použití v|
|----------|---------------------|----------|
|**Spustit nebo pokračovat**|F5|Podokno skriptu, při ladění skriptu|
|**Krok do**|F11|Podokno skriptu, při ladění skriptu|
|**Krok přes**|F10|Podokno skriptu, při ladění skriptu|
|**Krok**|SHIFT + F11|Podokno skriptu, při ladění skriptu|
|**Zásobník volání zobrazení**|CTRL + SHIFT + D|Podokno skriptu, při ladění skriptu|
|**Seznam zarážky**|CTRL + SHIFT + L|Podokno skriptu, při ladění skriptu|
|**Přepnout zarážku**|F9|Podokno skriptu, při ladění skriptu|
|**Odeberte všechny zarážky**|CTRL + SHIFT + F9|Podokno skriptu, při ladění skriptu|
|**Zastavení ladicího programu**|SHIFT + F5|Podokno skriptu, při ladění skriptu|

> ![Poznámka:](../core-powershell/web-access/images/Note.jpeg)**Poznámka**
>
> Můžete také použít klávesové zkratky určené pro konzolu prostředí Windows PowerShell při ladění skriptů v systému Windows PowerShell ISE. Chcete-li použít tyto klávesové zkratky, musí zadejte zástupce v podokně konzoly a stiskněte klávesu ENTER.

|Akce|Klávesové zkratky|Použití v|
|----------|---------------------|----------|
|**Pokračovat**|C|Podokna konzoly při ladění skriptu|
|**Krok do**|S|Podokna konzoly při ladění skriptu|
|**Krok přes**|V|Podokna konzoly při ladění skriptu|
|**Krok**|O|Podokna konzoly při ladění skriptu|
|**Zopakujte poslední příkaz** (pro krokování s vnořením nebo Krok přes)|ENTER|Podokna konzoly při ladění skriptu|
|**Zásobník volání zobrazení**|K|Podokna konzoly při ladění skriptu|
|**Zastavte ladění**|OTÁZKY|Podokna konzoly při ladění skriptu|
|**Seznam skriptu**|L|Podokna konzoly při ladění skriptu|
|**Zobrazení konzoly ladění příkazy**|H nebo?|Podokna konzoly při ladění skriptu|

## <a name="keyboard-shortcuts-for-windows-powershell-tabs"></a>Klávesové zkratky pro prostředí Windows PowerShell karty
Při použití karty prostředí Windows PowerShell můžete použít následující klávesové zkratky.

|Akce|Klávesové zkratky|
|----------|---------------------|
|**Zavřete kartu prostředí PowerShell**|CTRL + W|
|**Novou kartu prostředí PowerShell**|CTRL + T|
|**Předchozí kartu prostředí PowerShell**|CTRL + SHIFT + TAB. Tato zkratka funguje jenom v případě, že jsou na konkrétní kartě prostředí PowerShell otevřené žádné soubory.|
|**Další karta prostředí Windows PowerShell**|CTRL + TAB. Tato zkratka funguje jenom v případě, že jsou na konkrétní kartě prostředí PowerShell otevřené žádné soubory.|

## <a name="keyboard-shortcuts-for-starting-and-exiting"></a>Klávesové zkratky pro spuštění a ukončení
Můžete použít následující klávesové zkratky a spusťte konzolu prostředí Windows PowerShell (PowerShell.exe) nebo ukončíte Windows PowerShell ISE.

|Akce|Klávesové zkratky|
|----------|---------------------|
|**Ukončení**|ALT+F4|
|**Spustit PowerShell.exe** (konzola prostředí Windows PowerShell)|CTRL + SHIFT + P|

## <a name="see-also"></a>Viz také
- [Pomocí Windows PowerShell ISE](../core-powershell/ise/Using-the-Windows-PowerShell-ISE.md)

