---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Integrované skriptovací prostředí (ISE) v prostředí Windows PowerShell"
ms.assetid: f156b92d-0203-46d2-89c7-b4989d32e3d2
ms.openlocfilehash: 413fc375ad4617bfae59d6a1217cf9f91c2cf090
ms.sourcegitcommit: 05d576cf107780fa52b2db4a042816be40b00fbc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2018
---
# <a name="windows-powershell-integrated-scripting-environment-ise"></a>Integrované skriptovací prostředí (ISE) v prostředí Windows PowerShell

Systému Windows PowerShell Integrované skriptovací prostředí (ISE) je jedním ze dvou hostitelů pro modul prostředí Windows PowerShell a jazyk. S ním můžete napsat, spuštění a testování skriptů způsoby, které nejsou k dispozici v konzole Windows PowerShell. ISE přidá barevné zvýrazňování syntaxe, dokončování pomocí tabulátorů, IntelliSense, ladění visual a kontextovou nápovědu.

ISE umožňuje spouštět příkazy v podokně konzoly, ale také podporuje podokny, která vám pomůže současně zobrazit zdrojový kód vašeho skriptu a jiných nástrojů, které lze zařadit do ISE. I více skriptu Windows můžete otevřít ve stejnou dobu, která je zvlášť užitečné, pokud ladíte skript, který používá funkce definované v další skripty či moduly.

## <a name="whats-new"></a>Co je nového

Zde jsou některé funkce, které jsou přidané do ISE nejnovější verze prostředí PowerShell.

### <a name="added-in-powershell-30-windows-server-2012-windows-8"></a>Přidat v prostředí PowerShell 3.0 (Windows Server 2012, Windows 8)

**IntelliSense** zobrazením nabídky odpovídající rutiny, parametry, hodnoty parametrů, soubory nebo složky při psaní automaticky dokončení příkazech.

**Fragmenty kódu** krátké části kódu, který lze snadno vložit do skriptů vaší zápisu. Kolekce užitečné fragmenty kódu je součástí pole a více můžete pomocí **New-fragment** rutiny.

**Rozšíření nástrojů** přidá funkce, které mají ISE lze vytvořit pomocí psaní kódu, který komunikuje s [systému Windows PowerShell ISE skriptování objektový Model](../../core-powershell/ise/The-ISE-Object-Model-Hierarchy.md).

Tyto nástroje můžete zobrazit ovládací prvky v podokně s kartami nebo pracovat tedy bez zásahu uživatele na pozadí. **Příkazy** rozšíření je dobrým příkladem je součástí verze 3.0 a novější, který zobrazí seznam dostupných příkazů a jejich nápovědy.

**Restartujte Manager a automatického ukládání** automaticky uloží skripty každé dvě minuty, abyste nedošlo ke ztrátě práce v případě havárie nebo neočekávaně restartován.

**Seznam nejčastěji nedávno použité** je teď součástí soubor otevřete nabídku usnadňují získání k souborům nejčastěji.

**Sloučené podokna konzoly**. V předchozích verzích ISE byly samostatný příkaz a výstup podokna. Jsou nyní zkombinovány do jediné podokno, více přímo napodobuje co se zobrazí v konzole Windows Powershell.

**Přepínače příkazového řádku**. Několik nového přepínače příkazového řádku získáte tak větší kontrolu nad způsobu práce ISE. -NoProfile spustí ISE bez spuštění skriptu profilu. -Help otevře okno nápovědy s ISE. -mta spustí ISE v "režimu Vícevláknová apartment". Výchozí hodnota je jedním podprocesem.

**Nové funkce editor** usnadňují vytváření a čtení kódu:

- **Barevné zvýrazňování syntaxe XML**. Syntaxe jazyka XML ISE editor teď barvy stejným způsobem, jak ho barvy syntaxe kódu prostředí Windows PowerShell.

- **Odpovídající složené závorce**. ISEWindows PowerShell ISE označuje odpovídající složené závorky vám pomohou zajistit máte správný počet pravými tak, aby odpovídaly vaší otevírání těch, které jsou. Pomocí kombinace kláves CTRL -\[ najít pravé složené závorce, který odpovídá závorka, která se nachází kurzor na.

- **Zobrazení osnovy**. Můžete sbalit nebo rozšířit části kódu, kliknutím na znaménko plus a minus na levém okraji. Díky tomu je snazší najít kód, který hledáte ve dlouho skriptu.

- **Přetáhnout myší úpravy textu**. Můžete vybrat blok textu a přetáhněte ji do jiného umístění přesunout ho. Pokud podržíte stisknutou klávesu Ctrl a přetáhněte vybraný text, který je zkopírovat místo přesunete.

- **Analýza chybových zpráv**. Prostředí Windows PowerShell prověří váš skript během psaní. Pokud zjistí chybu, zobrazuje červenou vlnovkou pod problematické kódu. Po přesunutí ukazatele myši uvedené chyby, popisek znázorňuje problém, který nebyl nalezen.

- **Zvětšení**. Můžete přiblížit na vaše textu, aby bylo snazší pro čtení nebo oddálit a získat lepší náhled pomocí posuvníku v pravém dolním rohu okna ISE.

- **Rich text zkopírovat a vložit**. Když zkopírujete z ISE do schránky, písma, velikosti a barvy informace vybraného textu je zahrnuta.

- **Blokovat výběr**. Můžete vybrat bloku dat ve tvaru bloku textu, podržte stisknutou klávesu ALT a výběr textu v podokně skriptu s myší nebo stisknutím klávesy **Alt + Shift + šipka**.

### <a name="added-in-powershell-20-windows-server-2008-r2-windows-7"></a>Přidat v prostředí PowerShell 2.0 (Windows Server 2008 R2, Windows 7)

ISE byla zavedena v systému verze prostředí PowerShell 2.0.

## <a name="requirements-for-running-the-windows-powershell-ise"></a>Požadavky na spuštění Windows PowerShell ISE

ISE je k dispozici na libovolném počítači Windows, která se může spustit prostředí Windows PowerShell verze 2.0 nebo novější. Každou verzi Windows a Windows Server obsahuje verzi prostředí Windows PowerShell a ISE, ale můžete upgradovat na nejnovější verzi dostupnou instalací Windows Management Framework (WMF). Najdete v článku [WMF](/powershell/wmf/readme) Další informace naleznete v dokumentaci.

> [!NOTE]
> Protože Windows PowerShell ISE vyžaduje grafické uživatelské rozhraní, nelze jej spustit v jádra serveru systému Windows Server.

## <a name="see-also"></a>Viz taky

[Účelem ise windows power shell skriptování objektový model](../../core-powershell/ise/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
