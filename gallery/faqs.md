---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Nejčastější dotazy ke galerii prostředí PowerShell
ms.openlocfilehash: 3fa52892ce50491c040251baae8b4ae4ee3dcba0
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002868"
---
# <a name="frequently-asked-questions"></a>Nejčastější dotazy

## <a name="what-is-a-powershell-module"></a>Co je modul Powershellu?

Modul prostředí PowerShell se opakovaně použitelné balíček, který obsahuje některé funkce prostředí PowerShell. Všechno, co je v prostředí PowerShell (funkce, proměnné, prostředky DSC, atd.) se dá zabalit v modulech. Moduly jsou obvykle, složek, které neobsahují konkrétní typy souborů uložených v určité cestě. Existuje několik různých typů modulů Powershellu tam.

## <a name="what-is-a-powershell-script"></a>Co je skript prostředí PowerShell?

Skript prostředí PowerShell je řada příkazů, které jsou uložené v souboru .ps1 umožňují opakované použití a sdílení. Pracovní postupy Powershellu jsou také skriptů prostředí PowerShell, které popisují sadu úloh a poskytují pro tyto úlohy sekvencování. Další informace, navštivte prosím [Začínáme s pracovním postupem prostředí PowerShell](https://technet.microsoft.com/library/jj134242.aspx).

## <a name="how-are-powershell-scripts-different-from-powershell-modules"></a>Jak se liší od moduly Powershellu skripty prostředí PowerShell

Moduly jsou obecně vhodnější pro sdílení obsahu, ale jsme uvolnili skript sdílení zjednodušit přispívat pracovními postupy a skripty v komunitě. Další informace najdete v těchto blozích:

- [Nemusíte psát skripty, moduly Powershellu zápisu](https://blogs.technet.microsoft.com/heyscriptingguy/2011/06/27/dont-write-scripts-write-powershell-modules/)
- [Vysvětlení modulů Powershellu](https://blogs.technet.microsoft.com/heyscriptingguy/2015/07/10/understanding-powershell-modules/)

## <a name="how-can-i-publish-to-the-powershell-gallery"></a>Jak můžu publikovat v galerii prostředí PowerShell?

Před publikováním v galerii balíčků, je nutné zaregistrovat účet ve galerii prostředí PowerShell. Je to proto, že publikování balíčků vyžaduje NuGetApiKey, který získáte při registraci. Pokud chcete zaregistrovat, použijte osobní, pracovní nebo školní účet k přihlášení do Galerie prostředí PowerShell. Jednorázové registračním procesem je potřeba při prvním přihlášení. Později vaše NuGetApiKey je k dispozici na stránce svého profilu.

Jakmile budete zaregistrováni v galerii, použijte [Publish-Module](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) nebo [Publish-Script](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny pro publikování balíčku v galerii. Další podrobnosti o tom, jak tyto rutiny, přejděte na kartu publikovat nebo čtení [Publish-Module](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) a [Publish-Script](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) dokumentaci.

**Není potřeba registrovat nebo přihlásit do Galerie pro instalaci nebo uložení balíčků.**

## <a name="i-received-failed-to-process-request-the-specified-api-key-is-invalid-or-does-not-have-permission-to-access-the-specified-package-the-remote-server-returned-an-error-403-forbidden-error-when-i-tried-to-publish-a-package-to-the-powershell-gallery-what-does-that-mean"></a>Zobrazila se mi "nepovedlo se zpracovat požadavek. "Zadaný klíč rozhraní API je neplatný nebo nemá oprávnění pro přístup k zadanému balíčku.". Vzdálený server vrátil chybu: zakázáno (403). " Chyba při pokusu o publikování balíčku v galerii prostředí PowerShell. Co to znamená?

Této chybě může dojít z následujících důvodů:

- **Zadaný klíč rozhraní API je neplatný.**
     Zkontrolujte, zda jste zadali platný klíč rozhraní API z vašeho účtu. Pokud chcete získat klíč rozhraní API, zobrazte stránku svého profilu.
- **Název zadaný balíček není vlastníkem je.**
     Jestliže jste potvrdili, že svůj klíč rozhraní API správné, a může už existovat balík se stejným názvem jako ten, který se pokoušíte použít. Balíček mohly neuvedené vlastníkem, v takovém případě se nezobrazí žádné výsledky hledání. Pokud chcete zjistit, zda balíček se stejným názvem již existuje, otevřete prohlížeč a přejděte na stránku podrobností balíčku: `https://www.powershellgallery.com/packages/<packageName>`. Například, že přejdete přímo na `https://www.powershellgallery.com/packages/pester` se dostanete na stránce s podrobnostmi o Pester modulu, ať už jde o neuvedené v seznamu nebo ne. Pokud balíček konfliktní názvem již existuje a je neuvedené v seznamu, můžete:
    - Vyberte jiný název pro svůj balíček.
    - Obraťte se na vlastníky existující balíček.

## <a name="why-cant-i-sign-in-with-my-personal-account-but-i-could-sign-in-yesterday"></a>Proč se nemůžete zaregistrovat pomocí osobního účtu, ale může zaregistrovat včera?

Uvědomte si, že váš účet Galerie není přizpůsobuje změny vaší primární e-mailový alias. Další informace najdete v tématu [pouze aliasy společnosti Microsoft e-mailu](https://windows.microsoft.com/windows/outlook/add-alias-account).

## <a name="why-dont-i-see-all-the-gallery-packages-when-i-select-all-the-category-checkboxes-on-the-packages-tab"></a>Proč se po výběru kategorie políčka na kartě balíčky nevidíte všechny balíčky Galerie?

Výběrem zaškrtávacího políčka kategorie se uvede "Chci zobrazit všechny balíčky v této kategorii." Zobrazí se pouze balíčky vybraných kategorií. Proto podobně tak, že vyberete všechna zaškrtávací políčka kategorie, můžete se s informacemi o tom "Chci zobrazit všechny balíčky v každé kategorii." Ale některé balíčky v galerii nepatří do žádné z kategorií uvedených, takže se nezobrazí ve výsledcích. Pokud chcete zobrazit všechny balíčky v galerii, zrušte zaškrtnutí všech kategorií nebo znovu vyberte na kartě balíčky.

## <a name="what-are-the-requirements-to-publish-a-module-to-the-powershell-gallery"></a>Jaké jsou požadavky na publikování modulu v galerii prostředí PowerShell?

Jakýkoli druh modul PowerShell (moduly skriptu binární moduly a moduly manifestu), můžete ho publikovat v galerii. Publikování modulu PowerShellGet potřebuje vědět pár věcí o něm – verze, popis, autora a jakým způsobem je licencován. Tyto informace se číst jako součást procesu publikování z *manifestu modulu* souboru (.psd1), nebo od hodnoty [ **Publish-Module** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny **LicenseUri** parametru. Manifesty modul musí mít všechny moduly publikována do galerie. Libovolného modulu, který obsahuje tyto informace ve svém manifestu můžete publikovat v galerii:

- Verze
- Popis
- Autor
- Identifikátor URI pro licenční podmínky modulu, buď jako součást **PrivateData** části manifestu nebo v **LicenseUri** parametr [ **Publish-Module** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny.

## <a name="how-do-i-create-a-correctly-formatted-module-manifest"></a>Jak vytvořit modul správný formát manifestu?

Nejjednodušší způsob, jak vytvořit modul manifestu je spustit [ **New-ModuleManifest** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny. V Powershellu 5.0 nebo novější, New-ModuleManifest generuje manifest správně naformátovaný modulu s prázdnými poli pro užitečná metadata, jako je **ProjectUri**, **LicenseUri**, a **značky**. Stačí vyplnit prázdné znaky, nebo použijte vygenerovaný manifest s ukázkovým sice správné formátování.

Chcete-li ověřit, zda všechny požadované pole metadat byl správně zadán, použijte [ **testovací ModuleManifest** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny.

Chcete-li aktualizovat pole soubor manifestu modulu, použijte [ **aktualizace ModuleManifest** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny.

## <a name="what-are-the-requirements-to-publish-a-script-to-the-gallery"></a>Jaké jsou požadavky na publikování skript do Galerie?

Jakýkoli druh skript prostředí PowerShell (skripty nebo pracovních postupů), můžete ho publikovat v galerii. K publikování skript, musí správce balíčků PowerShellGet vědět pár věcí o něm – verze, popis, autora a jakým způsobem je licencován. Tyto informace se číst jako součást procesu publikování ze souboru skriptu *PSScriptInfo* oddílu, nebo od hodnoty [ **Publish-Script** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny  **LicenseUri** parametru. Informace o metadatech musí mít všechny skripty publikována do galerie. Žádný skript, který obsahuje tyto informace v části jeho PSScriptInfo mohou být publikovány do galerie:

- Verze
- Popis
- Autor
- Identifikátor URI s licenčními podmínkami skript jako součást **PSScriptInfo** části skriptu, nebo v **LicenseUri** parametr [ **Publish-Script** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny.

## <a name="how-do-i-search"></a>Jak mohu prohledávat?

Zadejte, co jste hledali v textovém poli. Například pokud chcete najít moduly, které se vztahují k Azure SQL, stačí zadáte "azure sql". Naše vyhledávací web bude hledat těchto klíčových slov ve všech publikovaných balíčků, včetně názvy, popisy a také napříč metadat. Potom podle skóre vážený kvality, zobrazí se nejbližší shody. Můžete také vyhledat pomocí konkrétní pole pomocí pole: "hodnota" syntaxe vyhledávacího dotazu pro následující pole:

- Značky
- Funkce
- Rutina
- DscResources
- Verze prostředí PowerShell

Ano, například při hledání verze prostředí PowerShell: zobrazí "2.0" pouze výsledky, které jsou kompatibilní s verze prostředí PowerShell 2.0 (podle jejich manifestu modulu nebo skriptu).

## <a name="how-do-i-create-a-correctly-formatted-script-file"></a>Jak vytvořit soubor skriptu správně naformátovaný?

Nejjednodušší způsob, jak vytvořit soubor skriptu správném formátu, který je spustit [ **New-ScriptFileInfo** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny. V Powershellu 5.0, New-ScriptFileInfo generuje soubor skriptu správný formát s prázdnými poli pro užitečná metadata, jako je **ProjectUri**, **LicenseUri**, a **značky** . Stačí vyplnit prázdné hodnoty nebo použít soubor generovaný skript jako příklad sice správné formátování.

Chcete-li ověřit, zda všechny požadované pole metadat byl správně zadán, použijte [ **testovací ScriptFileInfo** ](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny.

Chcete-li aktualizovat pole metadat skriptu, použijte [ **aktualizace ScriptFileInfo** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny.

## <a name="what-other-types-of-powershell-modules-exist"></a>Jaké existují jiné typy modulů Powershellu?

Modul Powershellu pojem také odkazuje na soubory, které implementují skutečné funkce. Soubory modulu skriptu (.psm1) obsahují kód Powershellu. Modul binární soubory (.dll) obsahují zkompilovaný kód.

Tady je jeden ze způsobů zamyslete o něm: složku, která zapouzdřuje modulu je složka modulu. Modul manifestu (.psd1), který popisuje obsah složky může obsahovat složku modulu. Soubory, které skutečně pracovat se soubory modulu skriptu (.psm1) a modulu binární soubory (.dll). Prostředky DSC se nacházejí v určité složce dílčí a jsou implementovány jako soubory modulu skriptu nebo binárního modulu.

Všechny moduly v galerii obsahují modul manifestů a většina z těchto modulů obsahuje soubory modulu skriptu nebo binárního modulu. Modul výraz může být matoucí kvůli tyto různé významy. Pokud není výslovně uvedeno jinak, všechny výskyty slova modulu na této stránce najdete složku modulu, která obsahuje tyto soubory.

## <a name="how-does-packagemanagement-relate-to-powershellget-high-level-answer"></a>Jak PackageManagement souvisí PowerShellGet? (Vysoké úrovně odpovědí)

PackageManagement je běžné rozhraní pro práci s všechny správce balíčků. Nakonec zda že pracujete s moduly Powershellu, souborů MSI, Ruby gems, balíčky NuGet a Perl modulů, byste měli moct pomocí příkazů v modulu PackageManagement (Najít balíček a Install-Package) najít a nainstalovat je. PackageManagement to dělá tak, že poskytovatel balíček pro každého správce balíčků, které zpřístupní PackageManagement. Poskytovatelé provést všechny skutečné práce; načíst obsah z úložiště a instalace obsahu místně. Poskytovatelé balíček často, jednoduše obtékat kolem stávající nástroje Správce balíčků pro typ daného balíčku.

Správce balíčků PowerShellGet je Správce balíčků pro balíčky prostředí PowerShell. Je zprostředkovatel PSModule balíček, který zpřístupňuje funkce Správce balíčků PowerShellGet pomocí modulu PackageManagement. Z toho důvodu můžete buď spustit [Install-Module](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) nebo Install-Package-PSModule zprostředkovatele k instalaci modulu z Galerie prostředí PowerShell. Některé funkce modulu PowerShellGet, včetně [Update-Module](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) a [Publish-Module](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409), není možné přistupovat prostřednictvím modulu PackageManagement příkazy.

Stručně řečeno Správce balíčků PowerShellGet výhradně fokus na s o premium balíčku prostředí pro správu obsahu prostředí PowerShell. PackageManagement se zaměřuje na vystavení všechny činnosti správy balíčků prostřednictvím obecné sadu nástrojů. Pokud tuto odpověď zjistíte unsatisfying, je v dlouhé odpovědí v dolní části tohoto dokumentu **jak PackageManagement skutečně souvisí PowerShellGet?** oddílu.

Další informace najdete [stránce projektu PackageManagement](https://oneget.org/).

## <a name="how-does-nuget-relate-to-powershellget"></a>Jak NuGet souvisí PowerShellGet?

Galerie prostředí PowerShell je upravená verze [Galerie NuGet](https://www.nuget.org/). Správce balíčků PowerShellGet používá NuGet zprostředkovatele pro práci s NuGet na základě úložišť jako galerie prostředí PowerShell.

Můžete použít Správce balíčků PowerShellGet proti žádné platné NuGet úložiště nebo sdílená složka. Stačí jednoduše přidat úložiště spuštěním [ **Register-PSRepository** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) rutiny.

## <a name="does-that-mean-i-can-use-nugetexe-to-work-with-the-gallery"></a>To znamená, že k práci pomocí galerie můžete použít NuGet.exe?

Ano.

## <a name="how-does-packagemanagement-actually-relate-to-powershellget-technical-details"></a>Jak PackageManagement skutečně souvisí PowerShellGet? (Podrobnosti)

Pod pokličkou Správce balíčků PowerShellGet využívá výraznou PackageManagement infrastruktury.

Ve vrstvě rutiny prostředí PowerShell [Install-Module](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) je ve skutečnosti dynamického zajišťování obálku kolem Install-Package-PSModule zprostředkovatele.

Ve vrstvě poskytovatele balíčku PackageManagement zprostředkovatel balíček PSModule skutečně zavolá do jiných poskytovatelů balíčku PackageManagement. Když pracujete s galerií založená na Nugetu (třeba Galerie prostředí PowerShell), zprostředkovatele PSModule balíčku používá poskytovatele balíčku NuGet pro práci s úložištěm.

![Architektura modulu PowerShellGet](Images/powershellgetArchitecture.png)

Obrázek 1: Architektura modulu PowerShellGet

## <a name="what-is-required-to-run-powershellget"></a>Co je potřeba ke spouštění Správce balíčků PowerShellGet?

Obecně doporučujeme vybrat nejnovější verzi modulu PowerShellGet (Všimněte si, že vyžaduje .NET 4.5).

**PowerShellGet** modul vyžaduje **prostředí PowerShell 3.0 nebo novější**.

Proto **PowerShellGet** vyžaduje jednu z následujících operačních systémů:

- Windows 10
- Windows 8.1 Pro
- Windows 8.1 Enterprise
- Windows 7 SP1
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2008 R2 SP1

**Správce balíčků PowerShellGet** také vyžaduje .NET Framework 4.5 nebo vyšší. Můžete nainstalovat rozhraní .NET Framework 4.5 nebo novější z [tady](https://msdn.microsoft.com/library/5a4x27ek.aspx).

## <a name="is-it-possible-to-reserve-names-for-packages-that-will-be-published-in-future"></a>Je možné rezervovat názvy balíčků, které se publikují v budoucnosti?

Není možné názvy turecké balíčků. Pokud se domníváte, že existující balíček obsazené název, který vyhovuje vašeho balíčku další, zkuste [kontaktovat vlastníka balíčku](./how-to/working-with-packages/contacting-package-owners.md). Pokud jste nedostali odpověď během pár týdnů, budete kontaktovat podporu a hledat v týmu Galerie prostředí PowerShell k němu.

## <a name="how-do-i-claim-ownership-for-packages"></a>Jak uplatním nárok na vlastnictví pro balíčky?

Podívejte se na [Správa vlastníků balíčku na PowerShellGallery.com](./how-to/publishing-packages/managing-package-owners.md) podrobnosti.

## <a name="how-do-i-deal-with-a-package-owner-who-is-violating-my-package-license"></a>Jak zacházet s vlastníka balíčku, který porušuje licenci na balíček

Doporučujeme komunity Powershellu spolupráce řešení všech sporů, které mohou vzniknout mezi vlastníky balíčku a vlastníci další balíčky.  Jsme vytvořený [spor proces překladu](./how-to/getting-support/dispute-resolution.md) , který vás požádáme o proveďte před intercede PowerShellGallery.com správci.
