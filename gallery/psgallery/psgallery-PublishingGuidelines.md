---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "Galerie prostředí powershell, rutiny, psgallery"
description: Pokyny pro vydavatele
title: "Galerie prostředí PowerShell publikování pokyny a osvědčené postupy"
ms.openlocfilehash: 882a33c00cc024ad2bbb05a3283e058a61035e3a
ms.sourcegitcommit: f069ff0689006fece768f178c10e3e3eeaee09f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/13/2017
---
# <a name="powershellgallery-publishing-guidelines-and-best-practices"></a>PowerShellGallery publikování pokyny a osvědčené postupy

Toto téma popisuje doporučené kroky používané Microsoft týmy zajistit položky publikované do Galerie prostředí PowerShell bude široce používat a uživatelům, založená na jak Galerie prostředí PowerShell zpracovává manifestu dat a na zpětnou vazbu od velké počty poskytnout vysoké hodnoty Galerie prostředí PowerShell uživatelů.
Položky, které jsou publikovány následující těchto pokynů bude více pravděpodobně nainstalována, důvěryhodný a přilákat více uživatelů.

Uvedeném níž jsou pokyny pro díky dobrý položky galerie prostředí PowerShell, volitelné manifestu nastavení, které jsou důležité, vylepšení kód s zpětnou vazbu od počáteční kontroloři a [analyzátor skriptu prostředí Powershell](https://aka.ms/psscriptanalyzer), Správa verzí vaše modulu, dokumentace, testy a příklady pro použití, co jste sdíleli.
Velká část této dokumentace se řídí pokyny pro publikování [vysoké kvality DSC prostředků moduly](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md).

Mechanismů publikování položky galerie prostředí PowerShell, najdete v části [vytváření a publikování položku](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/creating-and-publishing-an-item).

Je uvítali zpětná vazba týkající se těchto pokynů. Pokud máte zpětnou vazbu, otevřete prosím problémy v našem [úložiště Github dokumentaci](https://github.com/powershell/powershell-docs/).

## <a name="best-practices-for-publishing-items"></a>Osvědčené postupy pro publikování položek

Následující osvědčené postupy jsou, co uživatelé položek galerie Powershellu prohlašují, je důležité a jsou uvedeny v pořadí podle priority nominální.
Položky, které tato pravidla jsou mnohem pravděpodobnější se stáhnou a ostatní přijat.

* Použití PSScriptAnalyzer
* Zahrnují příklady a dokumentaci
* Spolupracovat s zpětné vazby
* Zadejte moduly spíše než skripty
* Zadejte odkazy na web projektu
* Zahrnout testy s moduly
* Zahrnují nebo propojit s licenčními podmínkami
* Podepisování kódu
* Postupujte podle [SemVer](http://semver.org/) pokyny pro správu verzí
* Použití běžných značek, jak je uvedeno v galerii prostředí PowerShell běžné značky
* Testování publikování pomocí místní úložiště

Každý z nich je stručně popsány v následujících částech.

## <a name="use-psscriptanalyzer"></a>Použití PSScriptAnalyzer

[PSScriptAnalyzer](https://www.powershellgallery.com/packages/PSScriptAnalyzer) je nástroj pro analýzu volné statické kódu, který funguje v prostředí PowerShell kód.
PSScriptAnalyzer určují nejběžnějších problémů zobrazená v kódu PowerShell a často doporučení, jak vyřešit problém.
Tento nástroj se snadno používá a rozděluje problémy jako chyby (závažné, je potřeba řešit), upozornění (třeba, aby a mělo by se řešit) a informace (vhodné kontrola osvědčených postupů).
Všechny položky položky publikované do Galerie prostředí PowerShell bude zkontrolovat pomocí PSScriptAnalyzer a všechny chyby budou hlášeny na vlastníka a je potřeba řešit.

Osvědčeným postupem je spustit `Invoke-ScriptAnalyzer` s `-Recurse` a `-Severity` upozornění.

Zkontrolujte výsledky a ujistěte se, že:

* Jsou všechny chyby opraveny nebo řešit v dokumentaci k
* Všechna upozornění jsou zkontrolovány a řešit, kde je to možné

Uživatelé, kteří získají položky z Galerie Powershellu jsou důrazně doporučujeme spustit PSScriptAnalyzer a vyhodnotit všechny chyby a upozornění.
Uživatelé budou velmi pravděpodobně Pokud uvidí, že dojde k chybě hlášené PSScriptAnalyzer kontaktujte vlastníci položky.
Pokud je přesvědčivý důvod pro položku kód, který je označena jako chyba, přidejte tyto informace k dokumentaci, abyste nemuseli odpověď na otázku stejné tolikrát, kolikrát.

## <a name="include-documentation-and-examples"></a>Zahrnují příklady a dokumentaci

Příklady a dokumentaci jsou nejlepší způsob, jak zajistit, aby uživatelé mohou využít výhod sdílené kód.

Dokumentace je užitečný zejména věcí, které chcete zahrnout do položky, které jsou publikovány do Galerie prostředí PowerShell.
Uživatelé budou obecně obejít položky bez dokumentace, jako je alternativním přečíst kód pochopit, co je položka a způsobu jeho použití.
Nejsou k dispozici na webu MSDN na tom, jak poskytnout dokumentaci s položkami prostředí PowerShell, včetně několika článcích:

* Pokyny pro poskytnutí nápovědy jsou v [postup nápovědě k rutině zápisu](https://go.microsoft.com/fwlink/?LinkID=123415)
* Vytvoření nápovědu rutiny, které je nejlepší metodou pro všechny skript prostředí PowerShell, funkci nebo rutinu.
  Informace o tom, jak vytvořit nápovědu rutiny, začínat [postup nápovědě k rutině zápisu](https://go.microsoft.com/fwlink/?LinkID=123415) v knihovně MSDN.
  Přidání nápovědy v rámci skriptu naleznete v tématu [o na základě nápovědy komentář](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_comment_based_help).
* Mnoho modulů také zahrnovat dokumentace v textovém formátu, například soubory MarkDown.
  To může být zvláště užitečné, když je web projektu v Githubu, kde je Markdownu vytíženou formát.
  Osvědčeným postupem je použít [Markdownu specifického pro Github](https://help.github.com/categories/writing-on-github/)

Příklady zobrazit uživatele, jak je položka určena k použití.
Celá řada vývojářů se dozvíte, se podívejte se na příklady před dokumentace pochopit, jak pomocí něčeho.
Nejlepší typ příklady zobrazit základní použití, plus případu použití simulované realistické a kód je dobře komentáři.
Příklady pro moduly, které jsou publikovány do Galerie prostředí PowerShell by měl být v příklady složce v kořenovém adresáři modulu.

Dobrý vzor příklady najdete v [PSDscResource modulu](https://www.powershellgallery.com/packages/PSDscResources) ve složce Examples\RegistryResource.
Existují čtyři ukázkové případy použití s stručný popis v horní části každého souboru této dokumenty, co je předmětem ukázky.

## <a name="respond-to-feedback"></a>Reagovat na připomínky

Vlastníci položky, kteří správně reagovat na připomínky jsou vysoce s hodnotou komunitou.
Uživatelé, kteří konstruktivní svůj názor jsou důležité reagovat, protože se jedná o zájem o dostatečně položka pokusit se je vylepšení.

Dvěma způsoby zpětnou vazbu k dispozici v galerii prostředí PowerShell:

* Kontaktujte vlastníka: Umožňuje uživatelům odeslat e-mail vlastníka/vlastníků položky. Jako položku vlastníka je důležité monitorovat e-mailovou adresu používat s položky galerie prostředí PowerShell a reagovat na problémy, které jsou vyvolány. K této metodě jeden nevýhodou je, že pouze uživatele a vlastník někdy uvidí komunikace, takže vlastník může mít odpověď na otázku stejné tolikrát, kolikrát.
* Poznámka: V dolní části stránky položky je pole komentář.
  Výhodou tohoto systému je, ostatní uživatelé mohou vidět komentáře a odpovědi, což snižuje počet, který musí být zodpovězeny všechny otázky, které jeden.
  Jako položku vlastníka důrazně doporučujeme postupujte podle na připomínky pro každou položku.
V tématu [poskytování zpětné vazby prostřednictvím sociálních médií nebo komentáře](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/psgallery-SocialMediaFeedback) podrobnosti o tom, jak to udělat.

Vlastníci, kteří reagovat na připomínky konstruktivně jsou zhodnotit komunitou.
Použít možnost v sestavě Pokud chcete požádat o další informace v případě potřeby, zadejte alternativní řešení, nebo určit, zda aktualizace řeší problém.

Pokud nevhodných chování zjištěnými z kterékoli z těchto komunikačních kanálů, obraťte se na správce Galerie pomocí funkce oznámení zneužití Galerie prostředí PowerShell.

## <a name="modules-versus-scripts"></a>Moduly a skripty

Sdílení s jinými uživateli skript řešení je skvělé a poskytuje další příklady, jak k řešení problémů, které můžou mít.
Problém je, že skripty v galerii prostředí PowerShell jednu soubory bez testy, příklady a speciální dokumentace.

Moduly Powershellu mít strukturu složek, která umožňuje více složek a souborů být součástí balíčku.
Struktura modulu umožňuje včetně jiných položek v seznamu jako nejlepší postupy: rutiny nápovědy, dokumentace, příklady a testy.
Největší nevýhodou je, že skript dovnitř modul musí být vystavený a použít jako funkce.
Informace o tom, jak vytvořit modul najdete v tématu [zápis modulu prostředí Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=144916).

Existují situace, kdy skript poskytuje lepší podmínky pro uživatele, zejména s konfigurací DSC.
Doporučený postup pro konfigurace DSC, je publikovat konfigurace jako skript doprovodné modulem, který obsahuje dokumenty, příklady a testy.
Skript obsahuje seznam doprovodné modulu pomocí RequiredModules = @(název modulu).
Tuto metodu lze použít u všech skriptů.

Samostatné skripty, které dodržujte doporučené postupy poskytují skutečné hodnoty ostatním uživatelům.
Pokud na základě komentáře dokumentace a odkaz na web projektu se důrazně doporučuje při publikování skript do Galerie prostředí PowerShell.

## <a name="provide-a-link-to-a-project-site"></a>Zadejte odkaz na web projektu

Web projektu je, kde mohou vydavatel komunikovat přímo s uživatelé ze svých položek galerie prostředí PowerShell.
Uživatelé přednost položky, které poskytují, jako je získat informace o položce snadněji umožňuje.
Mnoho položek v galerii prostředí PowerShell jsou vyvinuté v Githubu, další jsou poskytovány organizace s vyhrazenou webová služba.
Každá z těchto lze považovat za web projektu.

Přidání odkazu se provádí zahrnutím ProjectURI v části PSData manifestu:

        # A URL to the main website for this project.
        ProjectUri = 'https://github.com/powershell/powershell'

Pokud je k dispozici ProjectURI, galerie prostředí PowerShell obsahují odkaz na webu projekt na levé straně stránky položky.

## <a name="include-tests"></a>Zahrnout testy

Včetně testování pomocí kód open-source je důležité pro uživatele, protože je poskytuje záruku, o co ověříte a poskytuje informace o způsobu fungování vašeho kódu. Umožňuje také uživatelům Ujistěte se, že jejich není rozdělit původní funkce, pokud se upravit kód podle jejich prostředí.

Důrazně doporučujeme, aby testy zapsání využívat výhod Pester test rozhraní, které byla vytvořena speciálně pro prostředí PowerShell.
Pester je k dispozici v [Githubu](https://github.com/Pester/Pester), [Galerie prostředí PowerShell](https://www.powershellgallery.com/packages/Pester/)a dodává ve Windows 10, Windows Server 2016, WMF 5.0 a WMF 5.1.

[Pester web projektu na Githubu](https://github.com/Pester/Pester) zahrnuje dobrý dokumentaci na zápis Pester testy z Začínáme k osvědčené postupy.

Cíle pro test pokrytí jsou vyznačeny [dokumentaci vysoké kvality prostředků modulu](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md), s jednotkou 70 % testování doporučená pokrytí kódu.

## <a name="include-andor-link-to-license-terms"></a>Zahrnují nebo propojit s licenčními podmínkami

Všechny položky, které jsou publikovány do Galerie prostředí PowerShell musíte zadat licenční podmínky, nebo je vázán licence, které jsou součástí [podmínky použití](https://www.powershellgallery.com/policies/Terms) v části "Vykazuje A".
Nejlepší metodou k určení různých licenci je poskytnout odkaz na licence LicenseURI v PSData.
Příklad najdete v tématu Doporučená pole Manifest.

```powershell
PrivateData = @{
    PSData = @{

        # Tags applied to this module. These help with module discovery in online galleries.
        Tags = @('.net','acl','active-directory')

        # A URL to the license for this module.
        LicenseUri = 'http://www.apache.org/licenses/LICENSE-2.0'
```

## <a name="sign-your-code"></a>Podepisování kódu

Podepisování kódu poskytuje uživatelům s nejvyšší úroveň záruky, pro který publikované položky a že kopii kód získají přesně je co vydané vydavatele.
Další informace o obecně pro podpis kódu, najdete v části [Úvod k podepisování kódu](http://go.microsoft.com/fwlink/?LinkId=106296).
PowerShell podporuje ověřování prostřednictvím dvou primární přístupů pro podpis kódu:

* Podpis souborů skriptu
* Katalog podepisování modulu

Podpis souborů prostředí PowerShell je dobře zavedené přístup k zajištění, který kód spouštěna bylo vytvořeno pomocí spolehlivý zdroj a nebyl změněn.
Podrobnosti o tom, jak podepsat soubory skriptu prostředí PowerShell, najdete v článku [o podepisování](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_signing) tématu.
V přehledu lze přidat podpis žádnému. Soubor PS1, který ověří prostředí PowerShell při načtení skriptu.
Prostředí PowerShell může být omezen pomocí [zásady spouštění](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_execution_policies) rutiny k zajištění využití podepsané skripty.

Katalog podepisování moduly je funkce ve verzi 5.1 přidána do prostředí PowerShell.
Tom, jak podepsat modul, najdete v článku [katalogu rutiny](https://msdn.microsoft.com/en-us/powershell/wmf/5.1/catalog-cmdlets) tématu.
V přehledu podepisování katalogu je potřeba vytvořit soubor katalogu, která obsahuje hodnotu hash pro každý soubor v modulu, a pak tento soubor podpisového.
Publikování modulu PowerShellGet instalace modulu, uložit modulu a rutiny modulu aktualizace bude Kontrola podpisu zajistit, že je platná a pak potvrďte, že hodnota hash pro každou položku odpovídá, co je v katalogu.
Pokud je nainstalována předchozí verze modulu v systému, bude instalace modulu potvrďte, že podpisový autority pro novou verzi odpovídá dříve nainstalovaná.
Podepisování katalogu funguje s, ale nenahrazuje podepisování souborů skriptů. Prostředí PowerShell neověřuje katalog podpisů v okamžiku načtení modulu.

## <a name="follow-semver-guidelines-for-versioning"></a>Postupujte podle pokynů SemVer pro správu verzí

[SemVer](http://semver.org/) je veřejný názvů, který popisuje, jak struktury a změňte verze umožňující snadno výklad změny.
Verze pro vaše položky musí být součástí manifestu data.

* Verze by měl být strukturovaná jako 3 číselné bloky, které jsou odděleny tečkami jako 0.1.1 nebo 4.11.192
* "0" počínaje verzí znamenat, že položka není ještě produkční připravené a první číslo by měl začínat pouze s "0", pokud je číslo pouze použít
* Změny v první číslo (1.9.9999 k 2.0.0) označuje závažné a nejnovější změny mezi verzemi
* Změny v druhé číslo (1.01 k 1.02) označuje změny úrovni funkcí, jako je například přidávání nové rutiny do modulu
* Změny třetí číslo označuje pevné změny, jako je například nové parametry, ukázky aktualizované nebo nové testů
* Při výpisu verze, prostředí PowerShell seřadíte verze jako řetězce, takže 1.01.0 nakládáno jako větší než 1.001.0

Prostředí PowerShell se vytvořila před SemVer byla publikována, proto ji poskytuje podporu pro většinu, ale ne všechny elementy SemVer, konkrétně:

* Nepodporuje předprodejní řetězce v číslech verzí. To je užitečné, když chce poskytovat verze preview nového hlavní verze tohoto po zadání verze 1.0.0 vydavatel. To bude podporovaný v budoucí verzi rutiny Galerie prostředí PowerShell a PowerShellGet.
* Prostředí PowerShell a Galerie prostředí PowerShell povolit řetězce verze 1, 2 a 4 segmenty. Mnoho modulů časná není postupujte podle pokynů a verze produktů od společnosti Microsoft, uveďte sestavení informací 4th blokovat čísel (například 5.1.14393.1066). Z hlediska správy verzí tyto rozdíly jsou ignorovány.

## <a name="test-using-a-local-repository"></a>Testování pomocí místní úložiště

Galerie prostředí PowerShell nebyla navržena jako cíl pro testování procesu publikování.
Nejlepší způsob, jak otestovat začátku do konce proces publikování do Galerie prostředí PowerShell je nastavit a používat vlastní místní úložiště.
To lze provést několika způsoby, včetně:

* Nastavit místní instance Galerie prostředí PowerShell, pomocí [Galerie privátní PS projekt](https://github.com/PowerShell/PSPrivateGallery) v Githubu. Tento projekt preview vám pomůže nastavit instanci Galerie prostředí PowerShell, který můžete řídit a použití testů.
* Nastavení [interní úložiště Nuget](https://blogs.msdn.microsoft.com/powershell/2014/05/20/setting-up-an-internal-powershellget-repository/). To bude vyžadovat další práci nastavit, ale bude mít výhod ověřování několik dalších požadavků, zejména ověřování použití klíč rozhraní API, a zda závislosti jsou k dispozici v cílové při publikování.
* Nastavte sdílené složky jako test "úložiště". Toto je snadno nastavit, ale vzhledem k tomu, že je sdílené složky, ověření uvedených výše se neprovádí. Jednou z výhod potenciální v tomto případě je, že sdílené složky nekontroluje (povinné) klíč rozhraní API, abyste mohli používat stejné klíče byste k publikování do Galerie prostředí PowerShell.

S žádným z těchto řešení použijte k definování nového "úložiště", které používáte ve vlastnosti - úložiště pro publikování modul PSRepository registrace.

Jeden další bod o testovací publikování: nelze odstranit libovolnou položku publikovat do Galerie prostředí PowerShell, bez pomoci provozní tým, který bude potvrďte, že nic je závislé na položce, které chcete publikovat.
Z tohoto důvodu jsme nepodporují Galerie prostředí PowerShell jako testování cíl a libovolného vydavatele, který nemá tak bude kontaktovat.

## <a name="recommended-workflow"></a>Doporučené pracovního postupu

Většina úspěšné přístupů, které jsme našli pro položky, které jsou publikovány do Galerie prostředí PowerShell jsou tyto:

* Počáteční vývoj v stránku open source projektu. Prostředí PowerShell používá Githubu.
* Použít zpětnou vazbu od kontroloři a [analyzátor skriptu prostředí Powershell](https://aka.ms/psscriptanalyzer) získat kód na pevné stavu
* Zahrnout dokumentaci, tak ostatní vědět, jak používat práci
* Otestování publikování akci pomocí místní úložiště.
* Publikování stabilní nebo alfa vydání do Galerie prostředí PowerShell, a zkontrolujte, zda zahrnují dokumentaci a odkaz na váš web projektu
* Shromažďování zpětné vazby a iterovat kód ve vaší lokalitě projekt, a poté publikujte stabilní aktualizace do Galerie prostředí PowerShell
* Přidání příklady a Pester testů v projektu a modul
* Rozhodněte, pokud chcete kód podepsání vaší položky
* Pokud si myslíte, že projekt je připravený k použití v provozním prostředí, publikovat 1.0.0 verze do Galerie prostředí PowerShell
* Nadále shromažďování zpětné vazby a iterovat kódu založené na vstup uživatele
