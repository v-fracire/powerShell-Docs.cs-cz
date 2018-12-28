---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Přístupnost prostředí Windows PowerShell ISE
ms.assetid: a078f9d1-dd6b-4323-b16d-0622cd993aa8
ms.openlocfilehash: 78a001dbe43a0b005d10a817e05e4cc7a72f5bd0
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403718"
---
# <a name="accessibility-in-windows-powershell-ise"></a>Přístupnost prostředí Windows PowerShell ISE

Toto téma popisuje funkce usnadnění systému Windows Powershellu integrovaném skriptovacím prostředí (ISE), které mohou být užitečné.

* [Jak změnit velikost a umístění z podokna skriptu a konzoly](#how-to-change-the-size-and-location-of-the-console-and-script-panes)
* [Klávesové zkratky pro úpravy textu](#keyboard-shortcuts-for-editing-text)
* [Klávesové zkratky pro spouštění skriptů](#keyboard-shortcuts-for-running-scripts)
* [Klávesové zkratky pro přizpůsobení zobrazení](#keyboard-shortcuts-for-customizing-the-view)
* [Klávesové zkratky pro ladění skriptů](#keyboard-shortcuts-for-debugging-scripts)
* [Klávesové zkratky pro prostředí Windows PowerShell karty](#keyboard-shortcuts-for-windows-powershell-tabs)
* [Klávesové zkratky pro spuštění a ukončení](#keyboard-shortcuts-for-starting-and-exiting)

Společnost Microsoft se zavázala k tomu, aby vytvářela produkty a služby, jejichž používání je snadné pro každého. Následující témata obsahují informace o funkcích, produktech a službách, které usnadňují Windows PowerShell ISE přístupnější pro osoby s postižením.

Windows PowerShell ISE podporuje režim s vysokým kontrastem. Pro slabozraké zarážka informace jsou dostupné prostřednictvím rutin pro správu zarážky, jako například [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) a [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420). Další informace najdete v tématu "Jak spravovat zarážky" v [jak ladění skriptů v prostředí Windows PowerShell ISE](How-to-Debug-Scripts-in-Windows-PowerShell-ISE.md). Kromě funkcí a nástrojů usnadnění v Microsoft Windows následující funkce Ujistěte se, Windows PowerShell ISE přístupnější pro osoby s postižením:

- Klávesové zkratky

- Tabulka barevné zvýraznění syntaxe a schopnost upravovat několik dalších nastavení barev pomocí [$psISE.Options](https://technet.microsoft.com/library/75e2a76f-f3d1-490b-ad5d-e3829946aabb) objekt skriptování.

- Změna velikosti textu

## <a name="how-to-change-the-size-and-location-of-the-console-and-script-panes"></a>Jak změnit velikost a umístění z podokna skriptu a konzoly

Chcete-li změnit velikost a umístění v podokně konzoly a v podokně skriptu můžete použít následující postup. Když znovu otevřete Windows PowerShell ISE provedené změny velikosti a umístění zůstane zachovaná.

### <a name="to-resize-the-script-pane-and-console-pane"></a>Změna velikosti skriptovacím podokně a podokně konzoly

1. Pozastavte ukazatel myši na řádek rozdělit mezi skriptovacím podokně a podokně konzoly.

2. Při umístění ukazatele myši se změní na oboustrannou šipku, tažením změnit velikost podokna.

### <a name="to-move-the-script-pane-and-console-pane"></a>Chcete-li přesunout skriptovacím podokně a podokně konzoly

Udělejte jednu z těchto věcí:

- Přejděte v podokně skriptu nad podokně konzoly stiskněte **CTRL + 1** nebo na panelu nástrojů klikněte na tlačítko **zobrazit horní podokno skriptu** ikonu, nebo v **zobrazení** nabídky, klikněte na tlačítko **zobrazit Horní podokno skriptu**.

- Přejděte v podokně skriptu napravo od panelu konzoly stiskněte **CTRL + 2** nebo na panelu nástrojů klikněte na tlačítko **zobrazit pravé podokno skriptu** ikonu, nebo v **zobrazení** nabídky, klikněte na tlačítko **Zobrazit podokno skriptu správné**.

- Maximalizovat podokno skriptu, stiskněte klávesu **CTRL + 3** nebo na panelu nástrojů klikněte na tlačítko **zobrazit Maximalizovat podokno skriptu** ikonu, nebo **zobrazení** nabídky, klikněte na tlačítko **zobrazit skript Maximalizovat podokno**.

- Pro maximalizaci Pokokna konzoly a skrýt podokno skriptu na pravém okraji řádek karet, klikněte na tlačítko **skrýt podokno skriptu** ikonu v **zobrazení** nabídky, chcete-li zrušit výběr, klikněte **Zobrazitpodoknoskriptu** nabídky.

- Chcete-li zobrazit podokno skriptu, když v podokně konzoly maximalizované, na pravém okraji řádek karet, klikněte na tlačítko **zobrazit podokno skriptu** ikonu, nebo v **zobrazení** nabídky, zaškrtněte **zobrazit skript Podokno** nabídky.

## <a name="keyboard-shortcuts-for-editing-text"></a>Klávesové zkratky pro úpravy textu

Následující klávesové zkratky můžete použít, když upravujete textu.

|Akce|Klávesové zkratky|Použití v|
|----------|----------------------|----------|
|**Kopírování**|Ctrl + C|Skript nebo podokno konzoly|
|**Vyjmout**|CTRL + X|Skript nebo podokno konzoly|
|**Najít ve skriptu**|CTRL+F|Podokno skriptu|
|**Najít další ve skriptu**|F3|Podokno skriptu|
|**Najít předchozí ve skriptu**|SHIFT+F3|Podokno skriptu|
|**Vložit**|CTRL + V|Skript nebo podokno konzoly|
|**Znovu:**|CTRL + Y|Skript nebo podokno konzoly|
|**Nahraďte ve skriptu**|CTRL + H|Podokno skriptu|
|**Uložení**|CTRL+S|Podokno skriptu|
|**Vybrat vše**|CTRL + A|Skript nebo podokno konzoly|
|**Vrácení zpět**|CTRL + Z|Skript nebo podokno konzoly|

## <a name="keyboard-shortcuts-for-running-scripts"></a>Klávesové zkratky pro spouštění skriptů

Následující klávesové zkratky můžete použít při spouštění skriptů v podokně skriptu.

|Akce|Klávesové zkratky|
|----------|---------------------|
|**Nový**|CTRL + N|
|**Otevřít**|CTRL + O|
|**Spuštění**|F5|
|**Spustit výběr**|F8|
|**Zastavit provádění**|CTRL + BREAK. CTRL + C je možné, pokud kontext je jednoznačný (Pokud není vybraný žádný text).|
|**Karta** (pro další skriptu)|CTRL + TAB **Poznámka:** Kartu a další skript funguje pouze v případě, že máte do jedné karty Powershellu, otevřete, nebo pokud máte více než jedné karty Powershellu otevřít, ale je zaměřena tak, v podokně skriptu.|
|**Karta** (do předchozího skriptu)|CTRL + SHIFT + TAB **Poznámka:** Kartu předchozí skript funguje, pokud máte pouze jedna karta prostředí PowerShell otevřete, nebo pokud máte více než jedné karty Powershellu otevřít a fokus se v podokně skriptu.|

## <a name="keyboard-shortcuts-for-customizing-the-view"></a>Klávesové zkratky pro přizpůsobení zobrazení

Následující klávesové zkratky můžete použít k přizpůsobení zobrazení v prostředí Windows PowerShell ISE. Jsou přístupné ze všech podoken v aplikaci.

|Akce|Klávesové zkratky|
|----------|---------------------|
|**Přejděte do podokna konzoly**|CTRL + D|
|**Přejít na podokno skriptu**|CTRL + I|
|**Zobrazit podokno skriptu**|CTRL + R|
|**Skrýt podokno skriptu**|CTRL + R|
||
|**Podokno skriptu nahoru**|CTRL + 1|
|**Podokno skriptu doprava**|CTRL + 2|
|**Maximalizovat podokno skriptu**|CTRL + 3|
|**Přiblížit**|CTRL + SYMBOL PLUS|
|**Horizonální oddálení**|CTRL + MÍNUS|

## <a name="keyboard-shortcuts-for-debugging-scripts"></a>Klávesové zkratky pro ladění skriptů

Následující klávesové zkratky můžete použít při ladění skriptů.

|Akce|Klávesové zkratky|Použití v|
|----------|---------------------|----------|
|**Spustit/pokračovat**|F5|Podokno skriptu, při ladění skriptu|
|**Krokovat s vnořením**|F11|Podokno skriptu, při ladění skriptu|
|**Krok přes**|F10|Podokno skriptu, při ladění skriptu|
|**Krokovat s Vystoupením**|SHIFT+F11|Podokno skriptu, při ladění skriptu|
|**Zobrazení zásobníku volání**|CTRL+SHIFT+D|Podokno skriptu, při ladění skriptu|
|**Seznam zarážky**|CTRL+SHIFT+L|Podokno skriptu, při ladění skriptu|
|**Přepnout zarážku**|F9|Podokno skriptu, při ladění skriptu|
|**Odebrat všechny zarážky**|CTRL+SHIFT+F9|Podokno skriptu, při ladění skriptu|
|**Zastavit ladicí program**|SHIFT+F5|Podokno skriptu, při ladění skriptu|

> [!NOTE]
>
> Můžete také použít klávesové zkratky, určené pro konzolu prostředí Windows PowerShell při ladění skriptů v prostředí Windows PowerShell ISE. Pokud chcete použít tyto klávesové zkratky, musíte zadejte klávesovou zkratku v podokně konzoly a stiskněte klávesu ENTER.

|Akce|Klávesové zkratky|Použití v|
|----------|---------------------|----------|
|**Pokračovat**|C|Podokno konzole, při ladění skriptu|
|**Krokovat s vnořením**|S|Podokno konzole, při ladění skriptu|
|**Krok přes**|V|Podokno konzole, při ladění skriptu|
|**Krokovat s Vystoupením**|O|Podokno konzole, při ladění skriptu|
|**Opakovat poslední příkaz** (pro krok dovnitř nebo krok za)|ENTER|Podokno konzole, při ladění skriptu|
|**Zobrazení zásobníku volání**|TIS.|Podokno konzole, při ladění skriptu|
|**Zastavit ladění**|Q|Podokno konzole, při ladění skriptu|
|**Seznam skriptu**|L|Podokno konzole, při ladění skriptu|
|**Zobrazení konzole ladění příkazů**|H nebo?|Podokno konzole, při ladění skriptu|

## <a name="keyboard-shortcuts-for-windows-powershell-tabs"></a>Klávesové zkratky pro prostředí Windows PowerShell karty

Následující klávesové zkratky můžete použít při použití prostředí Windows PowerShell karty.

|Akce|Klávesové zkratky|
|----------|---------------------|
|**Zavřete kartu prostředí PowerShell**|CTRL + W|
|**Nová karta prostředí PowerShell**|CTRL + T|
|**Předchozí karta prostředí PowerShell**|CTRL+SHIFT+TAB. Tato zkratka funguje pouze v případě, že žádné soubory nejsou na libovolné kartě Powershellu otevřené.|
|**Další karta prostředí Windows PowerShell**|CTRL + TAB. Tato zkratka funguje pouze v případě, že žádné soubory nejsou na libovolné kartě Powershellu otevřené.|

## <a name="keyboard-shortcuts-for-starting-and-exiting"></a>Klávesové zkratky pro spuštění a ukončení

Následující klávesové zkratky můžete použít, spusťte konzolu Windows Powershellu (PowerShell.exe) nebo ukončete Windows PowerShell ISE.

|Akce|Klávesové zkratky|
|----------|---------------------|
|**Ukončení**|ALT+F4|
|**Spustit PowerShell.exe** (konzoly Windows Powershellu)|CTRL+SHIFT+P|

## <a name="see-also"></a>Viz také

[Představení Windows PowerShell ISE](Introducing-the-Windows-PowerShell-ISE.md)