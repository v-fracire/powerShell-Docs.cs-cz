---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutiny, psgallery
title: Nejčastější dotazy k Galerie prostředí PowerShell
ms.openlocfilehash: e377e71cf5eeb1f8b73430cc0b97527eac970cff
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="frequently-asked-questions"></a>Nejčastější dotazy

## <a name="what-is-a-powershell-module"></a>Co je modul Powershellu?

Modul prostředí PowerShell se opakovaně použitelné balíček obsahující některé funkce prostředí PowerShell. Vše v prostředí PowerShell (funkce, proměnné, prostředky DSC atd.) se dá zabalit v modulech. Moduly jsou obvykle složky obsahující konkrétní typy souborů uložených v konkrétní cesty. Existuje několik různých typů modulů Powershellu odhlašování došlo.

## <a name="what-is-a-powershell-script"></a>Co je skript prostředí PowerShell?

Skript prostředí PowerShell je řadu příkazů, které jsou uložené v souboru s příponou .ps1 povolení sdílení a opakované použití. Pracovní postupy prostředí PowerShell jsou také skripty prostředí PowerShell, které popisují sadu úloh a zadejte sekvencování pro tyto úlohy. Další informace najdete na webu [Začínáme s pracovním postupem prostředí PowerShell](https://technet.microsoft.com/library/jj134242.aspx).

## <a name="how-are-powershell-scripts-different-from-powershell-modules"></a>Jak se liší od moduly Powershellu skriptů prostředí PowerShell?

Moduly jsou obecně lepší pro sdílení, ale nemůžeme jsou povolení skriptu sdílení, aby bylo snazší pro vás přispívat pracovními postupy a skripty komunitě. Další informace najdete v těchto blozích:

- [Nemusíte psát skripty, moduly Powershellu zápisu](https://blogs.technet.microsoft.com/heyscriptingguy/2011/06/27/dont-write-scripts-write-powershell-modules/)
- [Seznámení s moduly prostředí PowerShell](https://blogs.technet.microsoft.com/heyscriptingguy/2015/07/10/understanding-powershell-modules/)

## <a name="how-can-i-publish-to-the-powershell-gallery"></a>Jak můžete publikovat do Galerie prostředí PowerShell?

Před publikováním položky do galerie, je nutné zaregistrovat účet v galerii prostředí PowerShell. Je to proto, že publikování položek vyžaduje NuGetApiKey, který je k dispozici při registraci. Pokud chcete zaregistrovat, použijte osobní pracovní nebo školní účet pro přihlášení do Galerie prostředí PowerShell. Jednorázové registraci je potřeba při prvním přihlášení. Vaše NuGetApiKey později, je k dispozici na stránce vašeho profilu.

Po registraci v galerii použít [publikovat modulu](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) nebo [publikovat skriptu](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutin do vaší položku publikovat do galerie. Další podrobnosti o tom, jak tyto rutiny spouštět, přejděte na kartu publikovat nebo číst [publikovat modulu](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) a [publikovat skriptu](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) dokumentaci.

**Není nutné registrace nebo přihlášení do Galerie pro instalaci nebo uložení položky.**

## <a name="i-received-failed-to-process-request-the-specified-api-key-is-invalid-or-does-not-have-permission-to-access-the-specified-package-the-remote-server-returned-an-error-403-forbidden-error-when-i-tried-to-publish-an-item-to-the-powershell-gallery-what-does-that-mean"></a>Zobrazila se "se nepodařilo zpracovat žádost. "K zadanému klíči rozhraní API je neplatný nebo nemá oprávnění k přístupu k zadanému balíčku.". Vzdálený server vrátil chybu: (403) zakázán. " Chyba při pokusu o publikování položky galerie prostředí PowerShell. Co to znamená?

Této chybě může dojít z následujících důvodů:

- **Zadaný klíč rozhraní API je neplatný.**
     Ujistěte se, zda jste zadali platný klíč rozhraní API z vašeho účtu. Získat klíč rozhraní API, zobrazte stránku profilu.
- **Název zadaný položky nevlastníte.**
     Jestliže jste potvrdili, který je správný klíč rozhraní API a potom možná již existuje položku se stejným názvem jako ten, který se pokoušíte použít. Položka možná neuvedené vlastníkem, v takovém případě se nezobrazí v žádné výsledky hledání. Pokud chcete zjistit, jestli položku se stejným názvem už existuje, otevřete prohlížeč a přejděte na stránce s podrobnostmi o položky: `https://www.powershellgallery.com/packages/<itemName>`. Například přejdete přímo na `https://www.powershellgallery.com/packages/pester` se dostanete na stránce s podrobnostmi o Pester modulu, jestli neuvedené nebo ne. Pokud položku konfliktní názvem již existuje a neuvedené, můžete:
    - Vyberte jiný název pro položku.
    - Obraťte se na vlastníci existující položku.

## <a name="why-cant-i-sign-in-with-my-personal-account-but-i-could-sign-in-yesterday"></a>Proč nelze I přihlásit pomocí mému osobnímu účtu, ale může přihlášení včera?

Upozorňujeme, že váš účet Galerie není zohlednit změny vaší primární e-mailový alias. Další informace najdete v tématu [aliasy e-mailu Microsoft](https://windows.microsoft.com/windows/outlook/add-alias-account).

## <a name="why-dont-i-see-all-the-gallery-items-when-i-select-all-the-category-checkboxes-on-the-items-tab"></a>Proč se po výběru kategorie políček na kartě položky nezobrazí všechny položky galerie?

Výběrem zaškrtávacího políčka kategorie jsou oznamující "Nastavit jako zobrazíte všechny položky v této kategorii." Zobrazí se pouze položky z vybraných kategorií. Proto podobně tak, že vyberete všechny kategorie políček, můžete se s informacemi o tom "Nastavit jako zobrazíte všechny položky v žádné kategorie." Ale některé položky v galerii nepatří do žádné z následujících kategorií, takže se nezobrazí ve výsledcích. Pokud chcete zobrazit všechny položky v galerii, zrušte zaškrtnutí všech kategorií nebo vyberte kartu položky znovu.

## <a name="what-are-the-requirements-to-publish-a-module-to-the-powershell-gallery"></a>Jaké jsou požadavky na publikování modul pro galerii prostředí PowerShell?

Jakýkoli druh modulu PowerShell (moduly skriptu, binární moduly nebo moduly manifestu) mohou být publikovány do galerie. K publikování modul, potřebuje PowerShellGet vědět pár věcí o něm - verze, popis, autora a jak je licencován. Tyto informace je přečíst jako součást procesu publikování z *modul manifestu* souboru (.psd1), nebo od hodnoty [ **publikovat modulu** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny **LicenseUri** parametr. Manifesty modul musí mít všechny moduly, které jsou publikovány do galerie. Libovolný modul, která obsahuje následující informace v manifestu lze publikovat do galerie:

- Verze
- Popis
- Autor
- Identifikátor URI pro licenční podmínky modulu, buď jako součást **PrivateData** oddílu manifest, nebo v **LicenseUri** parametr [ **Publish-Module** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny.

## <a name="how-do-i-create-a-correctly-formatted-module-manifest"></a>Vytvoření správně naformátován modul manifestu

Nejjednodušší způsob, jak vytvořit modul manifestu je spuštění [ **New-ModuleManifest** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny. V prostředí PowerShell 5.0 nebo novější, New-ModuleManifest generuje manifest správně naformátován modul s prázdné pole pro užitečné metadata jako **ProjectUri**, **LicenseUri**, a **značky**. Stačí vyplnit prázdné znaky, nebo použijte vygenerovaný manifest jako příklad správné formátování.

Chcete-li ověřit, že všechny požadované správně vyplněno pole metadat, použijte [ **Test ModuleManifest** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny.

Chcete-li aktualizovat pole souboru manifestu modulu, použijte [ **aktualizace ModuleManifest** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny.

## <a name="what-are-the-requirements-to-publish-a-script-to-the-gallery"></a>Jaké jsou požadavky na publikování skript do Galerie?

Jakýkoli druh skript prostředí PowerShell (skripty nebo pracovní postupy) mohou být publikovány do galerie. K publikování skript, potřebuje PowerShellGet vědět pár věcí o něm - verze, popis, autora a jak je licencován. Tyto informace je přečíst jako součást procesu publikování ze souboru skriptu *PSScriptInfo* oddílu, nebo od hodnoty [ **publikovat skriptu** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny  **LicenseUri** parametr. Informace o metadatech musí mít všechny skripty, které jsou publikovány do galerie. Žádný skript, který obsahuje tyto informace v jeho části PSScriptInfo lze publikovat do galerie:

- Verze
- Popis
- Autor
- Identifikátor URI s licenčními podmínkami skriptu, buď jako součást **PSScriptInfo** část skriptu, nebo v **LicenseUri** parametr [ **publikovat skriptu** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny.

## <a name="how-do-i-search"></a>Jak najít?

Zadejte, co hledáte v textovém poli. Například pokud chcete pro vyhledání modulů, které se vztahují k Azure SQL, stačí zadáte "azure sql". Naše vyhledávací web bude vypadat těchto klíčových slov v všechny položky publikované, včetně produktů, popisy a napříč metadat. Potom podle skóre vyvážené kvality, zobrazí na nejbližší odpovídá. Můžete také prohledat podle konkrétní pole pomocí pole: "value" syntaxe vyhledávacího dotazu pro následující pole:

- Značky
- Funkce
- Rutina
- DscResources
- Verze prostředí PowerShell

Ano, například při hledání verze prostředí PowerShell: "2.0" pouze výsledky, které jsou kompatibilní s verze prostředí PowerShell 2.0 (podle jejich manifestu modulu nebo skript) se zobrazí.

## <a name="how-do-i-create-a-correctly-formatted-script-file"></a>Jak vytvořit soubor správně naformátován skriptu?

Nejjednodušší způsob, jak vytvořit soubor správně naformátován skriptu je spuštění [ **New-ScriptFileInfo** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny. V prostředí PowerShell 5.0, New-ScriptFileInfo generuje soubor správně naformátován skriptu s prázdné pole pro užitečné metadata jako **ProjectUri**, **LicenseUri**, a **značky** . Stačí vyplnit prázdné znaky, nebo pomocí souboru generovaného skriptu jako příklad správné formátování.

Chcete-li ověřit, že všechny požadované správně vyplněno pole metadat, použijte [ **Test ScriptFileInfo** ](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny.

Chcete-li aktualizovat pole metadat skriptu, použijte [ **aktualizace ScriptFileInfo** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny.

## <a name="what-other-types-of-powershell-modules-exist"></a>Co existovat jiné typy modulů Powershellu?

Modul prostředí PowerShell termín také odkazuje na soubory, které implementují funkce skutečného. Soubory modulu skriptu (.psm1) obsahují kód, prostředí PowerShell. Modul binární soubory (.dll) obsahují zkompilovaný kód.

Tady je jedním ze způsobů myslíte o něm: složky, který zapouzdřuje modul je modulu. Složku modulu může obsahovat modul manifestu (.psd1), který popisuje obsah složky. Soubory, které ve skutečnosti práci se soubory modulu skriptu (.psm1) a modulu binární soubory (.dll). Prostředky DSC jsou umístěné v konkrétní podsložku a jsou implementované jako soubory modulu skriptu nebo modul binární soubory.

Všechny moduly v galerii obsahovat manifesty modulu a většina tyto moduly obsahovat soubory modulu skriptu nebo modul binární soubory. Modul podmínek může být matoucí kvůli tyto různé významy. Pokud není výslovně uvedeno jinak, všechny používá modul word na této stránce najdete do modulu složky obsahující tyto soubory.

## <a name="how-does-packagemanagement-relate-to-powershellget-high-level-answer"></a>Jak PackageManagement vztahují k PowerShellGet? (Vysoké úrovně odpovědí)

PackageManagement je společné rozhraní pro práci s všechny správce balíčků. Nakonec zda že pracujete s prostředí PowerShell, souborů MSI, Ruby gems, balíčky NuGet nebo moduly Perl, nyní byste měli mít používat příkazy pro PackageManagement (Najít balíček a Install-Package) můžete najít a nainstalovat je. PackageManagement tomu tak, že zprostředkovatel balíček pro každého správce balíčků, která po zapojení do PackageManagement. Zprostředkovatelé udělejte všechny samotnou práci; načíst obsah z úložiště a nainstalovat obsah místně. Zprostředkovatelé balíček často, jednoduše obtékat kolem existující nástroje Správce balíčku pro typ daného balíčku.

PowerShellGet je Správce balíčků pro položky prostředí PowerShell. Není zprostředkovatel PSModule balíček, který zveřejňuje funkce PowerShellGet prostřednictvím PackageManagement. Z toho důvodu můžete buď spustit [instalace modulu](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) nebo Install-Package-zprostředkovatele PSModule k instalaci modulu z Galerie prostředí PowerShell. Některé dílčí funkce PowerShellGet včetně [aktualizace modulu](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) a [publikovat modulu](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409), nelze získat přístup prostřednictvím PackageManagement příkazy.

Souhrnně PowerShellGet výhradně se zaměřuje na kterých se prostředí vždy premium balíček správy obsahu prostředí PowerShell. PackageManagement se zaměřuje na vystavení všechny činnosti správy balíček prostřednictvím obecné sadu nástrojů. Pokud zjistíte, tato odpověď unsatisfying, je v dlouho odpovědí v dolní části tohoto dokumentu **jak PackageManagement ve skutečnosti souvisí s PowerShellGet?** části.

Další informace naleznete [stránce projektu PackageManagement](https://oneget.org/).

## <a name="how-does-nuget-relate-to-powershellget"></a>Jak NuGet vztahují k PowerShellGet?

Galerie prostředí PowerShell je upravenou verzi [Galerie NuGet](https://www.nuget.org/). PowerShellGet používá zprostředkovatele NuGet pro práci s úložiště NuGet, na základě jako galerie prostředí PowerShell.

Můžete vytvořit PowerShellGet proti žádné platné NuGet úložiště nebo sdílené složky. Jednoduše je potřeba přidat úložiště spuštěním [ **Register-PSRepository** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny.

## <a name="does-that-mean-i-can-use-nugetexe-to-work-with-the-gallery"></a>Znamená to, že k práci s galerii můžete použít NuGet.exe?

Ano.

## <a name="how-does-packagemanagement-actually-relate-to-powershellget-technical-details"></a>Jak PackageManagement ve skutečnosti souvisí PowerShellGet? (Technické podrobnosti)

Pod pokličkou PowerShellGet výraznou využívá infrastrukturu PackageManagement.

Ve vrstvě rutiny prostředí PowerShell [instalace modulu](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) ve skutečnosti dynamické obálku kolem Install-Package-PSModule zprostředkovatele.

Ve vrstvě PackageManagement balíček zprostředkovatele volá zprostředkovatele balíček PSModule ve skutečnosti do jiných poskytovatelů PackageManagement balíčku. Při práci s na základě NuGet Galerie (třeba Galerie prostředí PowerShell), balíček zprostředkovatele PSModule používá zprostředkovatele balíčku NuGet pro práci s úložišti.

![Architektura PowerShellGet](Images/powershellgetArchitecture.png)

Obrázek 1: Architektura PowerShellGet

## <a name="what-is-required-to-run-powershellget"></a>Co je potřeba spustit PowerShellGet?

Obecně doporučujeme výběr nejnovější verzi modulu PowerShellGet (Všimněte si, že vyžaduje .NET 4.5).

**PowerShellGet** module vyžaduje **prostředí PowerShell 3.0 nebo novější**.

Proto **PowerShellGet** vyžaduje jednu z následujících operačních systémů:

- Windows 10
- Windows 8.1 Pro
- Windows 8.1 Enterprise
- Windows 7 SP1
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2008 R2 SP1

**PowerShellGet** taky vyžaduje rozhraní .NET Framework 4.5 nebo novější. Můžete nainstalovat rozhraní .NET Framework 4.5 nebo novější z [zde](https://msdn.microsoft.com/library/5a4x27ek.aspx).

## <a name="is-it-possible-to-reserve-names-for-items-that-will-be-published-in-future"></a>Je možné rezervovat názvy pro položky, které budou publikovány v budoucnosti?

Není možné názvy Turecká položek. Pokud si myslíte, že stávající položku vzalo na další, zkuste to název, který vyhovuje vaší položky [kontaktovat vlastníka položky](./how-to/working-with-items/contacting-item-owners.md). Pokud jste neobdrželi odpověď v rámci několik týdnů, obraťte se na podporu a k němu bude zkontrolujte týmem Galerie prostředí PowerShell.

## <a name="how-do-i-claim-ownership-for-items-"></a>Jak nárokovat vlastnictví pro položky?

Podívejte se na [Správa vlastníků položky na PowerShellGallery.com](./how-to/publishing-items/managing-item-owners.md) podrobnosti.

## <a name="how-do-i-deal-with-an-item-owner-who-is-violating-my-item-license"></a>Řešení s položky vlastníka, který je porušení Moje položky licenční smlouvy

Doporučujeme komunity Powershellu spolupracovat na řešení sporů, které může způsobit mezi vlastníky položek a vlastníků jiných položek.  Budeme mít vytvořené [proces řešení sporu](./how-to/getting-support/dispute-resolution.md) , vás požádáme o provedete před intercede PowerShellGallery.com správci.