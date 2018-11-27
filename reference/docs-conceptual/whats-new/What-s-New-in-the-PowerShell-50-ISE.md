---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Co je nového ve PowerShell 5.0 ISE
ms.assetid: 38648d47-7c27-4b37-a40e-ad29948519c2
ms.openlocfilehash: f05e3f3f95c8ceec6e843b8a1c79e6f092e1b87b
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320580"
---
# <a name="what39s-new-in-the-windows-powershell-ise"></a>Co&#39;nového ve Windows PowerShell ISE
Toto téma popisuje nové a aktualizované funkce, které byly zavedeny ve verzích systému Windows Powershellu integrovaném skriptovacím prostředí (ISE).

## <a name="feature-description"></a>Popis funkce
Windows PowerShell ISE je hostitelská aplikace, která umožňuje zapisovat, spouštět a testovat skripty a moduly v grafickém jednoduchá a intuitivní prostředí. Kartu klíčových funkcí, jako je například barevné zvýrazňování syntaxe, dokončování, vizuální ladění, dodržování předpisů kódování Unicode a kontextová nápověda poskytují celou řadu možností skriptování.

Přehled Windows PowerShell ISE, naleznete v tématu [přehled Windows Powershellu Integrované skriptovací prostředí](https://technet.microsoft.com/library/3c1892c2-bf84-4cb6-af26-1f453be9e671).

## <a name="new-and-changed-functionality-in-windows-powershell-ise"></a>Nové a změněné funkce v prostředí Windows PowerShell ISE
Následující tabulka uvádí nové a změněné funkce pro tuto verzi Windows PowerShell ISE v prostředí Windows PowerShell.

|Vlastnost/funkce|Windows PowerShell ISE 4.0|Windows PowerShell ISE 3.0|ISE Windows Powershellu 2.0|
|--------------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
|**[IntelliSense](#intellisense)**|X|X||
|**[Fragmenty kódu](#snippets)**|X|X||
|**[Doplňkové nástroje](#add-on-tools)**|X|X||
|**[Správce restartování a automatického ukládání](#restart-manager-and-auto-save)**|X|X||
|**[Seznam naposledy použitých](#most-recently-used-list)**|X|X||
|**[Podokně konzoly](#console-pane)**|X|X||
|**[Přepínače příkazového řádku](#command-line-switches)**|X|X||
|**[Nové funkce editoru](#new-editor-features)**|X|X||
|**[Nová okna programu Help viewer](#new-help-viewer-window)**|X|X||
|**[Rutiny show-– příkaz](#show-command-cmdlet)**|X|X||

### <a name="intellisense"></a>Technologie IntelliSense
**Přidáno v ISE 3.0**

Technologie IntelliSense je funkce automatického dokončování pomoc, který je součástí Windows PowerShell ISE. Technologie IntelliSense zobrazí po kliknutí nabídky potenciálně odpovídajících rutin, parametry, hodnoty parametrů, soubory nebo složky při psaní.

**Jakou hodnotu tato změna přináší?**

Přidání technologie IntelliSense je jednodušší zjistit rutiny a syntaxe, použijete-li vytvořit skripty Windows PowerShell ISE. Můžete také použít Windows PowerShell ISE další prostředí Windows PowerShell při vytváření nové skripty.

**Co funguje jinak?**

Po zadání rutiny Windows PowerShell ISE 3.0 nebo novější posuvný a kliknout, čímž nabídce se zobrazí, umožňuje procházet a vyberte příslušné příkazy.

### <a name="snippets"></a>Fragmenty kódu
**Přidáno v ISE 3.0**

*Fragmenty kódu* jsou krátké části kód prostředí Windows PowerShell, který můžete vložit do skriptů v prostředí Windows PowerShell ISE vytvoříte. Windows PowerShell ISE přednastavena výchozí fragmentů kódu. Fragmenty kódu můžete přidat pomocí **New-fragment** rutiny při práci v prostředí Windows PowerShell ISE.

**Jakou hodnotu tato změna přináší?**

Pomocí fragmentů kódu můžete rychle sestavit a vytvářet skripty pro automatizaci prostředí.

**Co funguje jinak?**

Na použití fragmenty kódu v prostředí Windows PowerShell 3.0 nebo novější, **upravit** nabídky, klikněte na tlačítko **spustit fragmenty**, nebo stiskněte klávesu **Ctrl-J**.

### <a name="add-on-tools"></a>Doplňkové nástroje
**Přidáno v prostředí PowerShell 3.0**

Windows PowerShell ISE teď podporuje doplněk nástroje, které jsou ovládacích prvků Windows Presentation Foundation (WPF), které jsou přidány pomocí objektového modelu. Doplňkové nástroje lze zobrazit jako svislý nebo vodorovný podokno v konzole. Více nástrojů pro doplněk v podokně se zobrazují jako ovládací prvek s kartami. Můžete také přidat nebo odebrat doplňkové nástroje, které jsou vytvářeny stranami mimo společnost Microsoft. Další informace o tom, jak importovat nebo odebrání nástrojů pro doplněk, naleznete v tématu [operacích Windows Powershellu ISE](https://technet.microsoft.com/library/cc732148.aspx).

**Jakou hodnotu tato změna přináší?**

Doplňky umožňují rozšířit a přizpůsobit pomocí nástrojů, které můžete vylepšení prostředí pro skriptování, nebo přidat funkci Windows PowerShell ISE Windows PowerShell ISE.

**Co funguje jinak?**

Prostředí Windows PowerShell ISE 3.0 a novější se dodávají s **příkazy** doplněk. **Příkazy** doplněk vám umožní procházet rutiny a nápovědu o rutiny – souběžně s **skript** a **konzoly** podoken.

Další doplňky můžete najít pomocí **otevřít webovou stránku nástroje pro doplněk** příkaz **doplňky** nabídky.

### <a name="restart-manager-and-auto-save"></a>Restartovat správce a automatického ukládání
**Přidáno v prostředí PowerShell 3.0**

Windows PowerShell ISE nyní automaticky ukládá otevřít skripty každé dvě minuty v samostatném umístění.  Pokud Windows PowerShell ISE přestane fungovat, nebo pokud operační systém se restartuje, po restartování prostředí Windows PowerShell ISE, obnoví otevřít skripty, které byly během poslední relace, i v případě, že skripty nebyly uloženy.

Pokud chcete změnit interval automatické ukládání, spusťte následující příkaz na panelu konzoly: **$psise. Options.AutoSaveMinuteInterval**.

**Jakou hodnotu tato změna přináší?**

Teď můžete pracovat v rámci Windows PowerShell ISE vědomím, že jsou otevřené skripty automaticky uložené v případě neočekávaného restartování.

**Co funguje jinak?**

Windows PowerShell ISE 2.0 nelze uložit skripty automaticky v případě restartování.

### <a name="most-recently-used-list"></a>Seznam naposledy použitých
**Přidáno v prostředí PowerShell 3.0**

Windows PowerShell ISE teď má seznam naposledy použitých souborů. Při otevření souboru v prostředí Windows PowerShell ISE, soubor je přidán do seznamu naposledy použitých na **souboru** nabídky.

Chcete-li změnit výchozí počet souborů v seznamu naposledy použitých, spusťte následující příkaz na panelu konzoly: **$psise. Options.MruCount**.

**Jakou hodnotu tato změna přináší?**

Seznam naposledy použitých teď můžete snadno přístup k souborům se často používá.

**Co funguje jinak?**

Windows PowerShell ISE 2.0 nemá seznam naposledy použitých.

### <a name="console-pane"></a>Podokně konzoly
**Přidáno v prostředí PowerShell 3.0**

Samostatný příkaz a výstupní podokna, které byly k dispozici v první verzi Windows PowerShell ISE byly zkombinovány do jediného konzoly. V podokně konzoly je podobné jako u funkce a vzhled typické konzoly Windows Powershellu, ale zahrnuje následující vylepšení (většina jsou popsány v tomto tématu).

- Barevné zvýrazňování syntaxe pro vstupního textu (ne výstupní text), včetně syntaxe jazyka XML

- Technologie IntelliSense

- Párování závorek

- Označení chyb

- Plná podpora kódování Unicode

- **F1** kontextové nápovědy

- **CTRL + F1** kontextové Show-– příkaz

- Složitým a podporu zprava doleva

- Podpora písma

- Přiblížení

- Režimy výběru řádku a výběru bloku

- Zachování zadaný obsah na příkazovém řádku po stisknutí klávesy **nahoru** šipku a zobrazte historii v konzole

**Jakou hodnotu tato změna přináší?**

Přidání těchto změn podokně konzoly poskytuje prostředí skriptování, který je konzistentní s rozhraní konzoly.

**Co funguje jinak?**

Windows PowerShell ISE 2.0 má samostatný příkaz a výstupní podokna.

### <a name="command-line-switches"></a>Přepínače příkazového řádku
**Přidáno v prostředí PowerShell 3.0**

Pokud spustíte z příkazového řádku Windows PowerShell ISE (zadáním **powershell_ise.exe**), můžete přidat následující nové přepínače příkazového řádku.

- *-NoProfile*: spuštění Windows PowerShell ISE bez spuštění **$profile**

- *-Help*: Zobrazí okno nápovědy

- *-mta*: spuštění Windows PowerShell ISE v režimu apartmentu s více vlákny. Výchozí režim operace pro Windows PowerShell ISE je jednovláknový apartment režimu nebo *- sta*.

**Jakou hodnotu tato změna přináší?**

Přidání přepínačů příkazového řádku umožňuje řízení prostředí, ve kterém běží Windows PowerShell ISE.

**Co funguje jinak?**

Windows PowerShell ISE 2.0 nedokáže rozpoznat tyto přepínače příkazového řádku.

### <a name="new-editor-features"></a>Nové funkce editoru
**Přidáno v prostředí PowerShell 3.0**

Další úpravy funkce Windows PowerShell ISE zahrnují:

- **Barevné zvýrazňování syntaxe XML**Windows PowerShell ISE teď barvy syntaxe jazyka XML stejným způsobem, jak barvy syntaxe prostředí Windows PowerShell.

- **Párování závorek** Windows PowerShell ISE zahrnuje párování složených závorek a zvýrazňování a je možné následujícím způsobem: (například pomocí **přejít na shodu** příkazu nebo **Ctrl +]** vyhledá pravé složené závorky, pokud máte vybrané levá složená závorka).

- **Zobrazení osnovy** podokně se skriptem podporuje sbalování, který umožňuje sbalení nebo kliknutím na tlačítko plus nebo mínus rozbalení části kódu přihlásí na levém okraji. Můžete použít složené závorky nebo **#region** a **#endregion** značky k označení začátku nebo konci do sbalitelného oddílu. Chcete-li rozbalit nebo sbalit všechny oblasti, stiskněte **Ctrl + M**.

- **Přetáhnout myší úpravy textu**ISE Windows PowerShell teď podporuje přetažení úpravy textu. Můžete vybrat libovolný blok textu a přetáhněte tento text do jiného umístění v editoru nebo konzoly pro přesunutí text. Pokud podržíte stisknutou klávesu Ctrl při přetahování vybraný text při uvolnění tlačítka myši text je zkopírován do nového umístění. V této verzi systému Windows PowerShell ISE, stejně jako v předchozí verzi Windows PowerShell ISE Když přetahujete soubory na Windows PowerShell ISE Windows PowerShell ISE otevře soubor.

- **Analýza chybových** chybami Parsování jsou označeny červenou vlnovkou. Když najedete myší uvedené chyby, zobrazí text popisku problém, který byl nalezen v kódu.

- **Přiblížení** procento zvětšení konzoly "™ s obsahem lze nastavit pomocí posuvníku lupy (v pravém dolním rohu okno integrovaného skriptovacího prostředí Windows PowerShell) nebo zadáním příkazu **$psise.options.Zoom** v podokně konzoly.

- **Formátovaný text zkopírovat a vložit** kopírování do schránky ve Windows PowerShell ISE zachová písmo, velikost a informace o barvě původní výběru.

- **Běr bloku** můžete vybrat blok textu, podržte stisknutou klávesu ALT a výběr textu v podokně skriptu pomocí myši nebo stisknutím klávesy **Alt + Shift + šipka**.

**Jakou hodnotu tato změna přináší?**

Další funkce úprav poskytovat konzistentní a výkonné prostředí pro úpravy.

**Co funguje jinak?**

Tyto úpravy vylepšení nebyly přítomny v rozhraní Windows PowerShell ISE 2.0.

### <a name="new-help-viewer-window"></a>Nová okna programu Help viewer
**Přidáno v prostředí PowerShell 3.0**

Pokud stisknete **F1** při kurzor je v rutině, nebo máte součástí rutiny zvýrazněný, nového programu Help viewer, otevře se kontextové nápovědy o rutině zvýrazněné. Chcete-li zobrazit nápovědu Windows Powershellu o, zadejte **operátory** v podokně konzoly a poté stiskněte klávesu **F1**.

Před použitím této funkce, stáhněte si nejnovější verze témata nápovědy pro Windows PowerShell na webu společnosti Microsoft. Nejjednodušší způsob stahování témata nápovědy je spustit **Update-Help** rutiny v podokně konzoly při spuštění Windows PowerShell ISE jako správce.

Kde je možné změnit **F1** klíče hledá nápovědy. V **nástroje**/**možnosti** nabídky na **obecné nastavení** ve skupině **další nastavení**, můžete nastavit nebo zrušte zaškrtávací políčko **nahrazujícím obsah místní nápovědy online obsah**. Pokud je zaškrtnuto, klient vyhledá pro rutinu Nápověda v nápovědě stažené nacházejí ve složce modulů.  Pokud políčko není zaškrtnuto, klient vyhledá v knihovně TechNet pro nápovědy k rutinám.

**Jakou hodnotu tato změna přináší?**

Kontextová nápověda, aniž byste museli opustit aktuální rutiny nebo skriptu poskytuje bezproblémové učení.

**Co funguje jinak?**

Stisknutím klávesy F1 v předchozích verzích Windows PowerShell ISE otevřít soubor nápovědy v místním počítači. Ve Windows Powershellu ISE 3.0 a novějších otevře se okno, které obsahuje nápovědu pro rutinu, která je prohledávatelná a je možné konfigurovat. Toto prostředí nápovědy je nová možnost instalace Windows PowerShell ISE 3.0 a aktualizovatelné nápovědy je nová možnost instalace Windows PowerShell 3.0.

### <a name="show-command-cmdlet"></a>Rutiny show-– příkaz
**Přidáno v prostředí PowerShell 3.0**

**Zobrazit příkaz** rutina umožňuje vytvořit nebo spustit rutiny nebo funkce vyplněním v grafické podobě. Formulář umožňuje uživatelům pracovat v prostředí Windows PowerShell v grafickém prostředí. **Zobrazit příkaz** také umožňuje používat pokročilé autory skriptů k vytvoření rychlého grafického rozhraní pomocí prostředí Windows PowerShell.

**Jakou hodnotu tato změna přináší?**

S použitím **zobrazit příkaz** ve skriptech prostředí Windows PowerShell můžete poskytnout uživatelům grafickém prostředí, ke kterému jsou známé. **Zobrazit příkaz** může také pomoct úvodní uživatelům naučit se prostředí Windows PowerShell.

**Co funguje jinak?**

Zobrazit příkaz je nový Windows PowerShell ISE 3.0.

## <a name="see-also"></a>Viz taky
Další informace o používání Windows PowerShell ISE v prostředí Windows PowerShell najdete v následujících tématech.

- [Zkoumání Windows Powershellu Integrované skriptovací prostředí](../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
- [ISE na wikiwebu TechNet](https://social.technet.microsoft.com/wiki/search/searchresults.aspx?q=ISE)
- [Centrum skriptů](https://technet.microsoft.com/scriptcenter/default)