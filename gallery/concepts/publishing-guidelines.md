---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
description: Pokyny pro vydavatele
title: Galerie prostředí PowerShell pro publikování pokyny a osvědčené postupy
ms.openlocfilehash: a996a820d6bd52e796a41659c6f468662dbff0f4
ms.sourcegitcommit: 548547b2d5fc73e726bb9fec6175d452a351d975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2018
ms.locfileid: "53655391"
---
# <a name="powershellgallery-publishing-guidelines-and-best-practices"></a>PowerShellGallery publikování pokyny a osvědčené postupy

Toto téma popisuje doporučené kroky, které Microsoft teams používají k zajištění balíčky publikována do Galerie prostředí PowerShell se široce přijat a poskytovat vysokou hodnotu pro uživatele, založené na zpracování manifestu dat v galerii prostředí PowerShell a na zpětnou vazbu z velké počet uživatelů Galerie prostředí PowerShell.
Balíčky, které jsou publikovány držet těchto pokynů bude větší pravděpodobnost nainstalované, důvěryhodný a přilákat více uživatelů.

Uvedeném níž jsou pokyny, co je dobré balíčku Galerie prostředí PowerShell, jaké volitelná nastavení manifestu jsou nejdůležitější, vylepšení kódu zpětnou vazbu z počáteční revidující a [analyzátoru skriptu prostředí Powershell](https://aka.ms/psscriptanalyzer), Správa verzí modulu, dokumentaci, testy a příklady pro použití, co jste sdíleli.
Velká část této dokumentace se řídí pokyny pro publikování [vysokou kvalitu DSC prostředků moduly](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md).

Mechanismus publikování balíčku v galerii prostředí PowerShell najdete v části [vytváření a publikování balíčku](/powershell/gallery/how-to/publishing-packages/publishing-a-package).

Názor na tyto pokyny je vítány. Pokud máte zpětnou vazbu, otevřete prosím problémy v našich [dokumentace k úložišti Github](https://github.com/powershell/powershell-docs/issues).

## <a name="best-practices-for-publishing-packages"></a>Osvědčené postupy pro publikování balíčků

Následující osvědčené postupy se, co uživatelé položky galerie prostředí PowerShell Řekněme, že je důležité a jsou uvedeny v pořadí podle priority nominální.
Balíčky, které postupujte podle následujících pokynů je mnohem pravděpodobnější ke stažení a ostatní společnosti.

- Použití PSScriptAnalyzer
- Zahrnout dokumentaci a příklady
- Možné reagovat na zpětnou vazbu
- Zadejte moduly, místo skriptů
- Poskytuje odkazy na projekt webu
- Označit váš balíček se kompatibilní PSEdition(s) a platformy 
- Zahrnout testy s moduly
- Zahrnout a/nebo propojit s licenčními podmínkami
- Podepisování kódu
- Postupujte podle [SemVer](http://semver.org/) pokyny pro správu verzí
- Použití běžných značek, jak je uvedeno v galerii prostředí PowerShell společné značky
- Test publikování pomocí místního úložiště
- Použití Správce balíčků PowerShellGet pro publikování

Každý z nich je stručně v následujících částech.

## <a name="use-psscriptanalyzer"></a>Použití PSScriptAnalyzer

[PSScriptAnalyzer](https://www.powershellgallery.com/packages/PSScriptAnalyzer) je nástroj pro analýzu statického kódu zdarma, která funguje na kód Powershellu.
PSScriptAnalyzer rozpoznají nejběžnějších problémů v kódu Powershellu a často doporučení, jak tento problém vyřešit.
Tento nástroj se snadno používá a slouží ke kategorizaci problémy jako chyby (závažnost, je potřeba řešit), varování (musí být zkontrolovány a mělo by se řešit) a informace (které stojí za to, rezervace osvědčených postupech pro).
Všechny balíčky, které jsou publikované v galerii prostředí PowerShell prohledá pomocí PSScriptAnalyzer a všechny chyby se předá zpátky na vlastníka, musí řešit.

Osvědčeným postupem je spuštění `Invoke-ScriptAnalyzer` s `-Recurse` a `-Severity` upozornění.

Zkontrolujte výsledky a ověřte, že:

- Všechny chyby jsou opraven nebo zákazníky a vyřešené v dokumentaci k sadě
- Všechna upozornění jsou zkontrolovány a řešit, kde je to možné

Uživatelé, kteří získají balíčků z Galerie prostředí PowerShell se důrazně doporučujeme spustit PSScriptAnalyzer a vyhodnotit všechny chyby a upozornění.
Uživatelé budou velmi pravděpodobně Pokud vidí, že je Chyba hlášená PSScriptAnalyzer obraťte se na vlastníky balíčku.
Pokud neexistuje závažný důvod pro váš balíček zachovat kód, který je označený jako chybu, přidejte tyto informace k dokumentaci, abyste se vyhnuli nutnosti odpověď na stejnou otázku v mnoha případech.

## <a name="include-documentation-and-examples"></a>Zahrnout dokumentaci a příklady

Dokumentaci a příklady jsou nejlepší způsob, jak zajistit, že uživatelé mohou využít výhod žádný sdílený kód.

Dokumentace je nejužitečnější věc, kterou chcete zahrnout do balíčků, které jsou publikované v galerii prostředí PowerShell.
Uživatelé budou obecně obejít balíčky bez dokumentaci, jak alternativou je načíst kód pochopit, co je balíček a jeho použití.
K dispozici několik článků o tom, jak poskytnout dokumentace ke službě pomocí prostředí PowerShell balíčků, včetně:

- Pokyny pro poskytnutí nápovědy jsou ve [jak nápovědě k rutině zápisu](https://go.microsoft.com/fwlink/?LinkID=123415)
- Vytváření nápovědy k rutinám, což je nejlepším řešením u skriptu, funkce nebo rutiny prostředí PowerShell.
  Informace o tom, jak vytvořit nápovědy k rutinám, začněte s [jak napsat nápovědě k rutině](https://go.microsoft.com/fwlink/?LinkID=123415).
  Přidání nápovědy v rámci skriptu naleznete v tématu [komentář na základě nápovědy](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).
- Mnoho modulů také zahrnout dokumentace v textovém formátu, jako jsou soubory Markdownu.
  To může být zvláště užitečné, když je web projektu na Githubu, kde je vytížený formátu Markdown.
  Osvědčeným postupem je použití [– Github-flavored Markdown](https://help.github.com/categories/writing-on-github/)

Příklady zobrazit uživatele, jak balíček je určena pro použití.
Mnoho vývojářů se dozvíte, že se podívejte se na příklady před dokumentaci, která pochopit, jak použít něco.
Nejlepší typ příklady zobrazit základní použití, a navíc případu použití s Simulovaná reálné a kód je dobře komentářem.
Příklady pro moduly, které jsou publikované v galerii prostředí PowerShell by měl být ve složce Příklady v kořenovém adresáři modulu.

Dobrý vzorek příklady lze nalézt v [PSDscResource modulu](https://www.powershellgallery.com/packages/PSDscResources) Examples\RegistryResource ve složce.
Existují čtyři ukázkové případy použití s stručný popis v horní části každého souboru dokumentující, co je právě jsme vám ukázali.

## <a name="respond-to-feedback"></a>Reakce na zpětnou vazbu

Balíček vlastníky, kteří správně reagovat na zpětnou vazbu jsou vysoce s hodnotou komunity.
Uživatelé, kteří poskytovat konstruktivní zpětnou vazbu jsou důležité pro reagovat, jako je zajímají dostatečně balíčku se pokouší Pomozte nám ji vylepšit.

V galerii prostředí PowerShell jsou k dispozici dvě metody zpětnou vazbu:

- Obraťte se na vlastníka: To umožňuje uživateli pošlete e-mail na počet vlastníků balíčku. Jako vlastníka balíčku je důležité monitorovat e-mailovou adresu používat s balíčky Galerie prostředí PowerShell a reagovat na problémy, které jsou vyvolány. Jednou nevýhodou této metodě se, že pouze uživatele a vlastník někdy zobrazí komunikace, takže vlastník může být nutné odpovědět na otázku, stejné v mnoha případech.
- Poznámka: V dolní části balíček stránka je pole komentář.
  Výhodou tohoto systému je, že další viděli komentáře a odpovědi, což snižuje počet pokusů, které se musí se odpovědět na každou otázku jeden.
  Jako vlastník balíčku důrazně doporučujeme, abyste postupovali podle připomínky pro každý balíček.
Zobrazit [poskytování zpětné vazby na sociálních sítích a v komentářích](../how-to/working-with-packages/social-media-feedback.md) podrobnosti o tom, jak to udělat.

Vlastníci, kteří konstruktivně reagovat na zpětnou vazbu jsou si vážíme komunitou.
Pomocí příležitosti v sestavě můžete požádat o další informace v případě potřeby, poskytují alternativní řešení a určit, jestli aktualizace opravuje problém.

Pokud je nevhodné chování v některé z těchto komunikačních kanálů, obraťte se na správce Galerie pomocí funkce ohlášení zneužití z Galerie prostředí PowerShell.

## <a name="modules-versus-scripts"></a>Moduly a skripty

Skript pro sdílení obsahu s ostatními uživateli se skvěle hodí a poskytuje další příklady toho, jak řešit problémy, které mohou mít.
Tento problém je, že skripty v galerii prostředí PowerShell jsou jednotlivé soubory bez speciální dokumentace, ukázky a testy.

Moduly Powershellu mít strukturu složek, která umožňuje více složek a souborů, které mají být zahrnuty s balíčkem.
Struktura modulu povolí, včetně dalších balíčků v seznamu osvědčených postupů: rutiny a dokumentaci, příklady a testy.
Největší nevýhodou je, že skript uvnitř modulu musí být vystavené a použít jako funkce.
Informace o tom, jak vytvořit modul najdete v tématu [zápis modulu prostředí Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=144916).

Existují situace, kdy skript poskytuje lepší prostředí pro uživatele, zejména s konfigurací DSC.
Osvědčeným postupem pro konfigurace DSC je publikovat konfiguraci jako skript pomocí doprovodných modulu, který obsahuje dokumentace, ukázky a testy.
Skript obsahuje doprovodné modulu s použitím RequiredModules = @(název modulu).
Tento přístup je možné u všech skriptů.

Samostatné skripty, které dodržujte doporučené postupy zadejte skutečné hodnoty ostatním uživatelům.
Poskytující založená na komentářích dokumentaci a odkaz na web projektu se důrazně doporučuje při publikování skript v galerii prostředí PowerShell.

## <a name="provide-a-link-to-a-project-site"></a>Zadejte odkaz na web projektu

Web projektu je, kde můžete vydavatel pracovat přímo s uživateli své balíčky Galerie prostředí PowerShell.
Uživatelé dávají přednost balíčky, které to umožňují, protože povoluje, abyste získali informace o balíčku snadněji.
Řada balíčků v galerii prostředí PowerShell jsou vyvíjeny v Githubu, ostatní jsou k dispozici organizacemi s vyhrazenou webová služba.
Každá z těchto lze považovat za web projektu.

Přidání propojení se provádí zahrnutím ProjectURI v části PSData manifestu:

        # A URL to the main website for this project.
        ProjectUri = 'https://github.com/powershell/powershell'

Pokud je k dispozici ProjectURI, galerie prostředí PowerShell bude obsahovat odkaz na web projektu na levé straně stránky balíčku.

## <a name="tag-your-package-with-the-compatible-pseditions-and-platforms"></a>Označit váš balíček se kompatibilní PSEdition(s) a platformy 

Pomocí následujících značek k předvedení pro uživatele, které balíčky budou fungovat s jejich prostředí:

- PSEdition_Desktop: Balíčky, které jsou kompatibilní s prostředím Windows PowerShell 
- PSEdition_Core: Balíčky, které jsou kompatibilní s Powershellu Core 
- Windows: Balíčky, které jsou kompatibilní s operačním systémem Windows
- Linux: Balíčky, které jsou kompatibilní s operačních systémů Linux 
- MacOS: Balíčky, které jsou kompatibilní se systémem Mac

## <a name="include-tests"></a>Zahrnout testy

Včetně testů s open source kódem je důležité uživatelům, protože mu zabezpečování, co můžete ověřit, nebo obsahuje informace o tom, jak kód funguje. Umožňuje také uživatelům zajistit, že nedojde k narušení váš původním funkce jejich úpravě kódu podle jejich prostředí.

Důrazně doporučujeme, že testy se zapisují využít rozhraní pro testování Pester, který byl určený speciálně pro prostředí PowerShell.
Pester je k dispozici v [Githubu](https://github.com/Pester/Pester), [Galerie prostředí PowerShell](https://www.powershellgallery.com/packages/Pester/)a dodává se ve Windows 10, Windows Server 2016, WMF 5.0 a WMF 5.1.

[Pester web projektu na Githubu](https://github.com/Pester/Pester) obsahuje dobrou dokumentaci k psaní testů Pester, od úvodního seznámení až osvědčené postupy.

Cíle pro pokrytí testu jsou uvedeny v [dokumentaci vysoké kvality prostředků modulu](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md), jednotku na 70 % pokrytí kódu doporučuje testu.

## <a name="include-andor-link-to-license-terms"></a>Zahrnout a/nebo propojit s licenčními podmínkami

Všechny balíčky, které jsou publikované v galerii prostředí PowerShell musíte zadat licenční podmínky, anebo byla vázaná podle licence, které jsou součástí [Terms of Use](https://www.powershellgallery.com/policies/Terms) v části "Dodatku A".
Nejlepší metodou k určení jiné licenční je poskytnout odkaz LicenseURI v PSData licenci.
Příklad najdete v tématu Doporučené Manifest pole.

```powershell
PrivateData = @{
    PSData = @{

        # Tags applied to this module. These help with module discovery in online galleries.
        Tags = @('.net','acl','active-directory')

        # A URL to the license for this module.
        LicenseUri = 'http://www.apache.org/licenses/LICENSE-2.0'
```

## <a name="sign-your-code"></a>Podepisování kódu

Podepisování kódu poskytuje uživatelům záruky pro vydavatele balíček na nejvyšší úrovni a, že kopie kódu získají je přesně to, co vydavatele všeobecně dostupné.
Další informace o obecně pro podepisování kódu, naleznete v tématu [Úvod k podepisování kódu](http://go.microsoft.com/fwlink/?LinkId=106296).
PowerShell podporuje ověřování prostřednictvím dvou přístupů primární pro podepisování kódu:

- Podepisování skriptů
- Katalog podepisování modulu

Podepisování souborů Powershellu je dobře zavedený přístup k zajištění toho, který se vytvořil parametrem spolehlivý zdroj prováděný kód a nebyl změněn.
Podrobnosti o tom, jak podepsat soubory skriptů prostředí PowerShell najdete v [o podepisování](/powershell/module/microsoft.powershell.core/about/about_signing) tématu.
V přehledu lze přidat podpis na žádné. Souboru PS1, která ověřuje Powershellu při načítání skriptu.
Prostředí PowerShell může být omezena pomocí [zásady spouštění](/powershell/module/microsoft.powershell.core/about/about_execution_policies) rutiny k zajištění využití podepsané skripty.

Podepisování moduly katalogu je funkce byly přidány do prostředí PowerShell ve verzi 5.1.
Jak zaregistrovat modul je obsažen v [katalogu rutiny](/powershell/wmf/5.1/catalog-cmdlets) tématu.
V přehledu podepisování katalogu se provádí vytváření soubor katalogu, který obsahuje hodnotu hash pro každý soubor v modulu, a pak podepíše soubor.
Publish-module PowerShellGet, install-module, save modulu a rutiny update-module se při kontrole podpisu zajistit, že je platný a potom potvrďte, že odpovídá hodnota hash pro každý balíček, co je v katalogu.
Pokud v systému je nainstalována předchozí verze modulu, install-module potvrdí, zda podpisový orgán pro novou verzi odpovídá dříve nainstalovali.
Podepisování katalogu funguje s, ale metoda nenahrazuje podepisování souborů skriptu. Prostředí PowerShell neověřuje katalog podpisů v okamžiku načtení modulu.

## <a name="follow-semver-guidelines-for-versioning"></a>Postupujte podle pokynů SemVer pro správu verzí

[SemVer](http://semver.org/) je veřejné konvence, která popisuje, jak strukturovat a změnit verzi umožňuje snadno výklad změny.
Verze balíčku musí být součástí manifestu data.

- Verze by měla být strukturovaná jako 3 číselné bloky, které jsou odděleny tečkami, stejně jako v 0.1.1 nebo 4.11.192
- Verze začíná "0" označuje, že balíček ještě není připravená pro výrobu a první číslo by měl pouze začínat "0" Pokud se jedná o jediný číslo použít
- Změny v první číslo (1.9.9999 na 2.0.0) označují hlavní a blokuje změny mezi verzí
- Změny v druhé číslo (1.01 k 1.02) označení změn na úrovni funkcí, jako je například přidávání nových rutin v modulu
- Změny třetí číslo označuje nevýznamných změn, jako jsou nové parametry, ukázky aktualizované nebo nové testy
- Při výpisu verze Powershellu seřadíte verze jako řetězce, takže 1.01.0, bude zacházeno jako větší než 1.001.0

Prostředí PowerShell byl vytvořen před SemVer byla publikována, proto ji poskytuje podporu pro většinu, ale ne všechny prvky semver, konkrétně:

- Předběžné verze řetězce nepodporuje v číslech verzí. To je užitečné, když chce poskytovat verze preview služby na novou hlavní verzi po zadání verze 1.0.0 vydavatele. Tato funkčnost bude podporovaná v budoucí verzi rutin Galerie prostředí PowerShell a Správce balíčků PowerShellGet.
- Prostředí PowerShell a Galerie prostředí PowerShell umožňují verze řetězce s 1, 2 a 4 segmentů. Mnoho modulů předčasné neřídil pokyny a verzích produktů od společnosti Microsoft zahrnují informace o sestavení, protože 4. blokovat čísel (například 5.1.14393.1066). Z hlediska správy verzí tyto rozdíly jsou ignorovány.

## <a name="test-using-a-local-repository"></a>Testování pomocí místního úložiště

Galerie prostředí PowerShell není navržena jako cíl pro testovací proces publikování.
Nejlepší způsob, jak otestovat na začátku do konce proces publikování v galerii prostředí PowerShell je nastavit a používat místního úložiště.
To můžete udělat několika způsoby, včetně:

- Nastavení místní instance Galerie prostředí PowerShell pomocí [PS privátní Galerie projektu](https://github.com/PowerShell/PSPrivateGallery) v Githubu. Tento projekt ve verzi preview vám pomůže nastavit instanci Galerie prostředí PowerShell, které lze řízeně a použití pro vaše testy.
- Nastavení [interní úložiště Nuget](https://blogs.msdn.microsoft.com/powershell/2014/05/20/setting-up-an-internal-powershellget-repository/). To bude vyžadovat další práce pro nastavení, ale bude mít výhodou ověřování několik dalších požadavků, zejména ověřování pomocí klíče rozhraní API a jestli se závislosti jsou k dispozici v cílové při publikování.
- Nastavení sdílené složky jako test "úložiště". Je to snadné nastavení, ale protože je sdílené složky, ověření, jak je uvedeno nahoře neproběhne. Jednou z výhod potenciální v tomto případě je, že sdílené složky souborů nekontroluje (povinné) klíč rozhraní API, abyste mohli používat stejné klíče byste to udělali publikovat v galerii prostředí PowerShell.

S žádným z těchto řešení použijte k definování nové "úložiště", který používáte pro Publish-Module-vlastnosti úložiště Register-PSRepository.

Jeden další bod o test publikování: všechny balíčky můžete publikovat v galerii prostředí PowerShell není možné odstranit bez pomoci od provozní tým, který bude tak jasné, že nic není závislá na balíčku, kterou chcete publikovat.
Z tohoto důvodu jsme nepodporují Galerie prostředí PowerShell jako cíl testování a kontaktuje libovolného vydavatele, který provádí.

## <a name="use-powershellget-to-publish"></a>Použití Správce balíčků PowerShellGet pro publikování

Důrazně doporučujeme, aby zdroje pomocí rutiny Publish-Module a Publish-Script při práci v galerii prostředí PowerShell.
Abyste se vyhnuli zapamatování důležité podrobnosti o instalaci z a publikování v galerii prostředí PowerShell se vytvořil správce balíčků PowerShellGet.
V některých případech vydavatelé jste se rozhodli PowerShellGet přeskočit a použít pro klienta NuGet nebo rutiny PackageManagement místo Publish-Module.
Existuje několik podrobností, které jsou snadno Zmeškali, což vede k širokou škálu žádosti o podporu.

Pokud je důvod, proč nelze použít Publish-Module nebo Publish-Script, prosím dejte vědět.
Založte problém v úložišti Githubu PowerShellGet a uveďte podrobnosti, které můžete vybrat NuGet nebo PackageManagement způsobují.

## <a name="recommended-workflow"></a>Doporučený pracovní postup

Nejúspěšnější přístup, který jsme našli pro balíčky, které jsou publikované v galerii prostředí PowerShell je následující:

- Počáteční vývoj v serveru projektu open source. Prostředí PowerShell tým používá Githubu.
- Použít zpětnou vazbu od recenzentů a [analyzátoru skriptu prostředí Powershell](https://aka.ms/psscriptanalyzer) získat kód do stavu stabilní
- Zahrnout dokumentace, takže ostatním vědět, jak použít svou práci
- Otestování publikování akce pomocí místního úložiště.
- Publikovat stabilní nebo alfa verze v galerii prostředí PowerShell, nezapomeňte použít dokumentaci a odkaz na vašem webu projectu
- Shromažďování zpětné vazby a iterovat kódu ve vašem webu projectu a potom publikovat stabilní aktualizace v galerii prostředí PowerShell
- Přidat příklady a Pester testů v projektu a modul
- Rozhodněte, jestli chcete kód podepsání vašeho balíčku
- Pokud se domníváte, že projekt je připravený k použití v produkčním prostředí, publikovat 1.0.0 verze v galerii prostředí PowerShell
- I nadále shromažďovat zpětnou vazbu a iterovat kódu na základě uživatelského zadání

