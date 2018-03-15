---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Jaké s 50 powershellu ISE"
ms.assetid: 38648d47-7c27-4b37-a40e-ad29948519c2
ms.openlocfilehash: 9fd25a4759602bebf2b5df2c17d0c816a15e5e2b
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="what39s-new-in-the-windows-powershell-ise"></a>Co&#39;s nová funkce v systému Windows PowerShell ISE
Toto téma popisuje nové a aktualizované funkce, které byly zavedeny ve verzích systému Windows PowerShell Integrované skriptovací prostředí (ISE).

## <a name="feature-description"></a>Popis funkce
Windows PowerShell ISE je hostitelskou aplikaci, která umožňuje zápis, spustit a otestovat skriptech a modulech v grafickém uživatelském rozhraní nebo intuitivní prostředí. Klíčové funkce, jako je například barevné zvýrazňování syntaxe, kartě dokončení, visual ladění, dodržování předpisů kódování Unicode a kontextová nápověda nabízí bohaté skriptovací prostředí.

Přehled Windows PowerShell ISE najdete v tématu [přehled Windows PowerShell Integrované skriptovací prostředí](https://technet.microsoft.com/library/3c1892c2-bf84-4cb6-af26-1f453be9e671).

## <a name="new-and-changed-functionality-in-windows-powershell-ise"></a>Nové a změněné funkce v systému Windows PowerShell ISE
Následující tabulka uvádí nové a změněné funkce pro tuto verzi systému Windows PowerShell ISE v prostředí Windows PowerShell.

|Vlastnost/funkce|Windows PowerShell ISE 4.0|Windows PowerShell ISE 3.0|Windows PowerShell ISE 2.0|
|--------------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
|**[IntelliSense](#intellisense)**|X|X||
|**[Fragmenty kódu](#snippets)**|X|X||
|**[Rozšíření nástrojů](#add-on-tools)**|X|X||
|**[Správce restartování a automatické ukládání](#restart-manager-and-auto-save)**|X|X||
|**[Seznam naposledy použitých](#most-recently-used-list)**|X|X||
|**[Podokna konzoly](#console-pane)**|X|X||
|**[Přepínače příkazového řádku](#command-line-switches)**|X|X||
|**[Nové funkce editoru](#new-editor-features)**|X|X||
|**[Nové okna programu Help viewer](#new-help-viewer-window)**|X|X||
|**[Zobrazit příkaz rutiny](#show-command-cmdlet)**|X|X||

### <a name="intellisense"></a>IntelliSense
**Přidat v integrovaném Skriptovacím 3.0**

IntelliSense je funkce Automatické dokončování pomoc, která je součástí systému Windows PowerShell ISE. IntelliSense zobrazí prokliknutelný nabídky potenciálně odpovídajících rutin, parametry, hodnoty parametrů, soubory nebo složky během psaní.

**Jakou přidanou hodnotu tato změna přináší?**

Po přidání IntelliSense je jednodušší zjistit rutiny a syntaxe při použití Windows PowerShell ISE vytvořit skripty. Windows PowerShell ISE můžete použít také další prostředí Windows PowerShell při vytváření nové skripty.

**Co funguje jinak?**

Když zadáte rutiny Windows PowerShell ISE 3.0 nebo novější, zobrazí nabídky posouvatelného a můžete kliknout, umožní vám procházet a vyberte příslušné příkazy.

### <a name="snippets"></a>Fragmenty kódu
**Přidat v integrovaném Skriptovacím 3.0**

*Fragmenty kódu* krátké části kód prostředí Windows PowerShell, který můžete vložit do skriptů, které vytvoříte v systému Windows PowerShell ISE. Windows PowerShell ISE se dodává s výchozí sadu fragmenty kódu. Fragmenty kódu můžete přidat pomocí **New-fragment** rutiny při práci s Windows PowerShell ISE.

**Jakou přidanou hodnotu tato změna přináší?**

Pomocí fragmenty kódu můžete rychle sestavit a vytvářet skripty pro automatizaci prostředí.

**Co funguje jinak?**

Na použití fragmenty kódu v prostředí Windows PowerShell 3.0 nebo novější, **upravit** nabídky, klikněte na **spustit fragmenty**, nebo stiskněte klávesu **Ctrl-J**.

### <a name="add-on-tools"></a>Rozšíření nástrojů
**Přidat v prostředí PowerShell 3.0**

Windows PowerShell ISE teď podporuje rozšíření nástroje, které jsou ovládací prvky Windows Presentation Foundation (WPF), které jsou přidané pomocí objektového modelu. Doplněk nástroje lze zobrazit jako svislé nebo vodorovné podokno v konzole. Několik rozšíření nástrojů v podokně se zobrazí jako záložkách ovládací prvek. Můžete také přidat nebo odebrat nástroje doplňků, které vytváří strany jiných společností než Microsoft. Další informace o tom, jak importovat nebo odebrání nástrojů pro rozšíření najdete v tématu [operace systému Windows PowerShell ISE](http://technet.microsoft.com/library/cc732148.aspx).

**Jakou přidanou hodnotu tato změna přináší?**

Rozšíření umožňují rozšířit a přizpůsobit Windows PowerShell ISE s nástroji, které mohou rozšířit možnosti skriptování nebo přidání funkcí do systému Windows PowerShell ISE.

**Co funguje jinak?**

Prostředí Windows PowerShell ISE 3.0 a novějších jsou součástí **příkazy** rozšíření. **Příkazy** rozšíření umožňuje procházet rutiny a získat přístup k nápovědě o rutiny-souběžného s **skriptu** a **konzoly** podokna.

Další doplňky můžete najít pomocí **otevřete doplněk Nástroje pro web** příkazu na **doplňky** nabídky.

### <a name="restart-manager-and-auto-save"></a>Restartujte manager a automatické ukládání
**Přidat v prostředí PowerShell 3.0**

Windows PowerShell ISE nyní automaticky uloží otevřete skripty každé dvě minuty, v samostatných umístění.  Pokud Windows PowerShell ISE přestane fungovat, nebo pokud je restartován operační systém, po restartování prostředí Windows PowerShell ISE, obnoví otevřete skripty, které byly v průběhu poslední relace, i v případě, že tyto skripty nebyly uloženy.

Pokud chcete změnit interval automatické ukládání, spusťte následující příkaz v podokně konzoly: **$psise. Options.AutoSaveMinuteInterval**.

**Jakou přidanou hodnotu tato změna přináší?**

Teď můžete pracovat v rámci systému Windows PowerShell ISE zároveň budete vědět, že otevřete skripty automaticky uloží v případě neočekávaného restartování.

**Co funguje jinak?**

Prostředí Windows PowerShell ISE 2.0 neuloží skripty automaticky v případě restartování.

### <a name="most-recently-used-list"></a>Seznam naposledy použitých
**Přidat v prostředí PowerShell 3.0**

Windows PowerShell ISE teď obsahuje seznam naposledy použitých souborů. Při otevření souboru v systému Windows PowerShell ISE, soubor je přidaný do seznamu naposledy použitých na **souboru** nabídky.

Chcete-li změnit výchozí počet souborů v seznamu naposledy použitých, spusťte následující příkaz v podokně konzoly: **$psise. Options.MruCount**.

**Jakou přidanou hodnotu tato změna přináší?**

Seznam naposledy použitých teď můžete snadno přístup k souborům se často používá.

**Co funguje jinak?**

Prostředí Windows PowerShell ISE 2.0 nemá seznam naposledy použitých.

### <a name="console-pane"></a>Podokna konzoly
**Přidat v prostředí PowerShell 3.0**

Samostatný příkaz i jeho podokna výstup, které byly dostupné v první verzi systému Windows PowerShell ISE sloučeny do jednoho podokna konzoly. V podokně konzoly je podobné funkce a vzhled typické konzoly prostředí Windows PowerShell, ale obsahuje následující vylepšení (většina jsou popsány v tomto tématu).

- Barevné zvýrazňování syntaxe pro vstupní text (není výstup text), včetně syntaxe jazyka XML

- IntelliSense

- Související závorky

- Označení chyb

- Plná podpora Unicode

- **F1** Kontextová nápověda

- **CTRL + F1** kontextová zobrazit – příkaz

- Komplexní skript a podpora zprava doleva

- Podpora písma

- Přiblížení

- Režimy řádku – vybrat a vyberte bloku

- Písmen a zachovávání s typem obsahu na příkazovém řádku při stisknutí volby **až** šipku zobrazení historie v konzole

**Jakou přidanou hodnotu tato změna přináší?**

Přidání těchto změn podokna konzoly poskytuje skriptovací prostředí, které je konzistentní s rozhraní konzoly.

**Co funguje jinak?**

Prostředí Windows PowerShell ISE 2.0 má samostatný příkaz a výstupní podokna.

### <a name="command-line-switches"></a>Přepínače příkazového řádku
**Přidat v prostředí PowerShell 3.0**

Pokud spustíte z příkazového řádku Windows PowerShell ISE (zadáním **powershell_ise.exe**), můžete přidat následující nové přepínače příkazového řádku.

- *-NoProfile*: spuštění systému Windows PowerShell ISE bez nutnosti spustit **$profile**

- *-Help*: Zobrazí okno nápovědy

- *-mta*: spustí ISE Windows PowerShell v režimu více vláken typu apartment. Single-threaded apartment režimu, je výchozí režim operace pro Windows PowerShell ISE nebo *- sta*.

**Jakou přidanou hodnotu tato změna přináší?**

Přidání tyto přepínače příkazového řádku umožňuje řídit prostředí, ve kterém se spouští Windows PowerShell ISE.

**Co funguje jinak?**

Prostředí Windows PowerShell ISE 2.0 nerozpoznal tyto přepínače příkazového řádku.

### <a name="new-editor-features"></a>Nové funkce editoru
**Přidat v prostředí PowerShell 3.0**

Další úpravy funkce systému Windows PowerShell ISE zahrnují:

- **Barevné zvýrazňování syntaxe XML**Windows PowerShell ISE teď barvy syntaxe jazyka XML stejným způsobem, jak ho barvy syntaxe prostředí Windows PowerShell.

- **Odpovídající složené závorce** Windows PowerShell ISE obsahuje odpovídající složené závorce a zvýraznění a je možné následujícím způsobem: (například pomocí **přejděte tak, aby shodu** příkaz nebo **Ctrl +]** vyhledá uzavírací závorku, pokud máte složená závorka vybrané).

- **Zobrazení osnovy** podokně skriptu podporuje osnovy, což umožňuje sbalení nebo rozbalení sekcí kódu kliknutím plus nebo minus přihlásí levým okrajem. Můžete použít složené závorky nebo **#region** a **#endregion** značky k označení začátku nebo konci sbalitelné části. Chcete-li rozbalit nebo sbalit všechny oblasti, stiskněte **kombinaci kláves Ctrl + M**.

- **Přetáhnout myší úpravy textu**ISE Windows PowerShell teď podporuje přetažení úpravy textu. Můžete vybrat všechny blok textu a přetáhněte tento text do jiného umístění v editoru nebo konzole přesunout text. Pokud podržíte stisknutou klávesu Ctrl a přetáhněte vybraný text po uvolnění tlačítka myši text zkopírován do nového umístění. V této verzi systému Windows PowerShell ISE, jakož i předchozí verzi systému Windows PowerShell ISE když jste přetažení soubory do systému Windows PowerShell ISE Windows PowerShell ISE otevře soubor.

- **Analýza chybových zpráv** analýzy chyby jsou označeny červenou podtržení. Po přesunutí ukazatele myši uvedené chyby, zobrazí se text popisku problém, který nebyl nalezen v kódu.

- **Zvětšení** procento přiblížení konzoly '™ s obsahu lze nastavit pomocí posuvníku přiblížení (v pravém dolním rohu okna Windows PowerShell ISE) nebo zadáním příkazu **$psise.options.Zoom** v podokně konzoly.

- **Rich text zkopírovat a vložit** kopírování do schránky v systému Windows PowerShell ISE uchovává písma, velikosti a barvy informace původní výběru.

- **Blokovat výběr** blok textu můžete vybrat, podržte klávesu ALT a výběr textu v podokně skriptu s myší nebo stisknutím klávesy **Alt + Shift + šipka**.

**Jakou přidanou hodnotu tato změna přináší?**

Další úpravy funkce poskytují více konzistentní a efektivní prostředí pro úpravy.

**Co funguje jinak?**

Tyto úpravy vylepšení nebyly nalezeny v prostředí Windows PowerShell ISE 2.0.

### <a name="new-help-viewer-window"></a>Nové okna programu Help viewer
**Přidat v prostředí PowerShell 3.0**

Pokud vyberete **F1** Pokud vaše kurzor se nachází v rutiny, nebo máte součástí rutiny zvýrazněná, nový prohlížeč nápovědy otevře kontextové nápovědy o rutině zvýrazněné. Chcete-li zobrazit nápovědu Windows PowerShell o, zadejte **operátory** v podokně konzoly a poté stiskněte klávesu **F1**.

Před použitím této funkce stažení nejnovější verze témat nápovědy prostředí Windows PowerShell na webu společnosti Microsoft. Nejjednodušší způsob stahování témata nápovědy je spuštění **Update-Help** rutiny v podokně konzoly při spuštění Windows PowerShell ISE jako správce.

Kde můžete změnit **F1** klíč hledá nápovědy. V **nástroje**/**možnosti** nabídky na **obecné nastavení** v části **další nastavení**, můžete nastavit nebo vymazat zaškrtávací políčko **používat místní obsah nápovědy místo obsahu online**. Pokud je zaškrtnuto, pak klient vyhledá rutinu Nápověda v nápovědě stažené nachází ve složce moduly.  Pokud není políčko zaškrtnuto, klient Hledat na nápovědu rutiny v knihovně TechNet.

**Jakou přidanou hodnotu tato změna přináší?**

Kontextová nápověda, aniž byste museli opustit váš aktuální rutiny nebo skriptu zajišťuje bezproblémové learning prostředí.

**Co funguje jinak?**

Stisknutím klávesy F1 v předchozích verzích systému Windows PowerShell ISE otevřít soubor nápovědy v místním počítači. V prostředí Windows PowerShell ISE 3.0 nebo novější otevře se okno obsahující nápovědu pro rutinu, která je s možností vyhledávání a konfigurovat. Toto prostředí nápovědy je nového pro prostředí Windows PowerShell ISE 3.0 a aktualizovatelné nápovědy je nového pro prostředí Windows PowerShell 3.0.

### <a name="show-command-cmdlet"></a>Zobrazit příkaz rutiny
**Přidat v prostředí PowerShell 3.0**

**Zobrazit příkaz** rutina umožňuje vytvořit nebo spouštět rutiny nebo funkce vyplněním grafických formulářů. Formulář umožňuje uživatelům práci s prostředím Windows PowerShell v grafickém prostředí. **Zobrazit příkaz** také umožňuje pokročilé autory skriptů vytvořit rychlé grafického rozhraní založené na prostředí Windows PowerShell.

**Jakou přidanou hodnotu tato změna přináší?**

Pomocí **zobrazit příkaz** v prostředí Windows PowerShell skripty, můžete poskytnout uživatelům grafické prostředí, ke kterému jsou známé. **Zobrazit příkaz** může také pomoci úvodní uživatelé další prostředí Windows PowerShell.

**Co funguje jinak?**

Zobrazit příkaz je nové prostředí Windows PowerShell ISE 3.0.

## <a name="see-also"></a>Viz taky
Další informace o používání v prostředí Windows PowerShell Windows PowerShell ISE najdete v následujících tématech.

- [Zkoumání Windows PowerShell Integrované skriptovací prostředí](../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
- [ISE na webu TechNet Wiki](http://social.technet.microsoft.com/wiki/search/searchresults.aspx?q=ISE)
- [Centra skriptů](http://technet.microsoft.com/scriptcenter/default)

