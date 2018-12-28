---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Integrované skriptovací prostředí ISE Windows Powershellu
ms.assetid: f156b92d-0203-46d2-89c7-b4989d32e3d2
ms.openlocfilehash: a5fcc8c813349d0b85cc3af29047424fe787d168
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403633"
---
# <a name="windows-powershell-integrated-scripting-environment-ise"></a>Integrované skriptovací prostředí (ISE) v prostředí Windows PowerShell

Windows Powershellu integrovaném skriptovacím prostředí (ISE) je mezi dvěma hostiteli pro modul prostředí Windows PowerShell a jazyk. S ní můžete zapisovat, spouštět a testovat skripty způsoby, které nejsou k dispozici v konzole Windows Powershellu. ISE přidá barevné zvýrazňování syntaxe, dokončování pomocí tabulátoru, technologie IntelliSense, ladění visual a kontextové nápovědy.

ISE umožňuje spouštění příkazů v podokně konzoly, ale také podporuje podoken, které můžete použít současně zobrazit zdrojový kód skriptu a dalších nástrojů, které se můžete zapojit do ISE. Ve stejnou dobu, což je zvláště užitečné při ladění skriptu, který používá funkce definované v jiné skripty a moduly můžete otevřít i více skriptů windows.

## <a name="whats-new"></a>Co je nového

Tady jsou některé funkce, které byly přidány do nejnovější verze prostředí PowerShell ISE.

### <a name="added-in-powershell-30-windows-server-2012-windows-8"></a>Přidáno v prostředí PowerShell 3.0 (Windows Server 2012, Windows 8)

**Technologie IntelliSense** zobrazením nabídky odpovídající rutiny, parametry, hodnoty parametrů, soubory nebo složky při psaní automaticky dokončí příkazům.

**Fragmenty kódu** jsou krátké části kódu, můžete jednoduše vložit do skriptů vaše zápisu. Kolekce užitečné fragmentů kódu je součástí pole a je možné pomocí více **New-fragment** rutiny.

**Doplňkové nástroje** přidá funkce, které chcete ISE mohou vytvořit psaní kódu, který komunikuje s [The Windows Powershellu objektový Model skriptování ISE](../../core-powershell/ise/The-ISE-Object-Model-Hierarchy.md).

Tyto nástroje můžete zobrazit ovládací prvky v podokně s kartami nebo transparentně pracovat na pozadí. **Příkazy** doplněk je typickým příkladem a je součástí verze 3.0 a novější, který zobrazí seznam dostupných příkazů a jejich nápovědy.

**Restartovat správce a automatického ukládání** automaticky uloží vaše skripty každé dvě minuty abyste se vyhnuli ztrátě práce v případě chyb nebo neočekávaného restartování.

**Seznam naposledy použitých nejčastěji** je teď součástí souboru otevřít nabídku, aby bylo snazší získat soubory, které použijete nejčastěji.

**Sloučené podokně konzoly**. V předchozích verzích ISE byly samostatný příkaz a výstupní podokna. Jsou nyní zkombinovány do jediného, že informace přímo napodobuje uvidíte v konzole Windows Powershellu.

**Přepínače příkazového řádku**. Několik nových přepínače příkazového řádku získáte větší kontrolu nad tím, jak funguje ISE. -NoProfile spustí ISE bez spuštění skriptu profilu. -Help otevře se okno nápovědy s ISE. -mta spustí ISE v "režimu vícevláknového objektu apartment". Výchozí hodnota je s jedním vláknem.

**Nové funkce editoru** bylo snazší vytvářet a číst váš kód:

- **Barevné zvýrazňování syntaxe XML**. Syntaxe jazyka XML ISE editor teď barvy stejným způsobem, jak barvy syntaxe kódu v prostředí Windows PowerShell.

- **Párování závorek**. Prostředí PowerShell ISE ISEWindows zvýrazní odpovídající složené závorky vám pomohou zajistit máte správný počet pravé složené závorky tak, aby odpovídaly úvodním těch, které jsou. Pomocí CTRL -\[ najít odpovídající levou složenou závorku, které se kurzor nachází na pravé složené závorce.

- **Zobrazení osnovy**. Můžete sbalit nebo rozbalit oddíly kódu kliknutím na tlačítko plus a minus na levém okraji. Díky tomu je snazší najít kód, který hledáte dlouhé skriptu.

- **Přetáhnout myší úpravy textu**. Můžete vybrat blok textu a přetáhněte ji do jiného umístění ji přesunout. Pokud podržíte stisknutou klávesu Ctrl při přetahování vybraný text, který je zkopírovat místo přesuňte.

- **Analýza chybových**. Prostředí Windows PowerShell prozkoumá váš skript při psaní. Pokud zjistí chybu, zobrazí červená vlnovka pod problematický kód. Když najedete myší uvedené chyby, popisek se dozvíte, problému, který nebyl nalezen.

- **Přiblížení**. Můžete přiblížit na vaše textu, aby bylo snazší pro čtení nebo oddálit, a prohlížení ve velkém s využitím posuvník v pravém dolním rohu okno integrovaného skriptovacího prostředí.

- **Formátovaný text zkopírovat a vložit**. Při kopírování z ISE do schránky, písmo, velikost a informace o barvě vybraného textu je v ceně.

- **Běr bloku**. Můžete vybrat blok textu ve tvaru bloku tím, že podržíte stisknutou klávesu ALT při výběru text z podokna skriptu pomocí myši nebo stisknutím klávesy **Alt + Shift + šipka**.

### <a name="added-in-powershell-20-windows-server-2008-r2-windows-7"></a>Přidáno v prostředí PowerShell 2.0 (Windows Server 2008 R2, Windows 7)

ISE byla zavedená s Powershellem v2.0.

## <a name="requirements-for-running-the-windows-powershell-ise"></a>Požadavky na spuštění Windows PowerShell ISE

ISE je dostupná na libovolném počítači Windows, který můžete spustit prostředí Windows PowerShell verze 2.0 nebo novější. Zahrnuje každá verze Windows a Windows Server na verzi prostředí Windows PowerShell ISE, ale můžete upgradovat na nejnovější verzi dostupnou instalací Windows Management Frameworku (WMF). Zobrazit [WMF](/powershell/wmf) Další informace naleznete v dokumentaci.

> [!NOTE]
> Protože Windows PowerShell ISE vyžaduje grafické uživatelské rozhraní, nelze ji spustit v jádra serveru systému Windows Server.

## <a name="see-also"></a>Viz taky

[Účel skriptovacího objektového modelu windows power shell ise](../../core-powershell/ise/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)