---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutiny, psgallery
title: Vytváření a publikování položky
ms.openlocfilehash: 7c2a2be6986bf65c168d7c3960366fac4ee31301
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189529"
---
# <a name="creating-and-publishing-an-item"></a>Vytváření a publikování položky

Galerie prostředí PowerShell je místo pro publikování a sdílení stabilní moduly Powershellu, skripty a prostředků DSC s širší komunita uživatelské prostředí PowerShell.

Tento článek se zabývá mechanismy a důležité kroky pro přípravu skript nebo modul a publikování do Galerie prostředí PowerShell.
Důrazně doporučujeme, abyste si prošli [pokyny pro publikování](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/psgallery-PublishingGuidelines) pochopit, jak zajistit, že položky můžete publikovat více široce přijme uživatelé Galerie prostředí PowerShell.

Jsou minimální požadavky na publikování položky galerie prostředí PowerShell:

- Máte účet Galerie prostředí PowerShell a klíč rozhraní API s ním spojená.
- Zkontrolujte, zda že je nutné Metadata v dané položce
- Ujistěte se, že vaše položka je připravena k publikování pomocí nástrojů pro předběžné ověření
- Publikování položky galerie prostředí PowerShell pomocí příkazů modulu publikování a publikovat skriptu
- Odpovídá na dotazy nebo pochybnostmi vaší položky

Galerie prostředí PowerShell přijme moduly prostředí PowerShell a skriptů prostředí PowerShell.
Když označujeme skripty, jsme znamená Powershellový skript, který je jeden soubor a není součástí větší modulu.

## <a name="powershell-gallery-account-and-api-key"></a>Galerie prostředí PowerShell účtu a klíč rozhraní API

V tématu [vytvoření účtu Galerie prostředí PowerShell](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/psgallery_creating_an_account) pro postup nastavení účtu Galerie prostředí PowerShell.

Po vytvoření účtu můžete získat klíč rozhraní API, které jsou potřebné k publikování položky.
Po přihlášení pomocí účtu své uživatelské jméno se zobrazí v horní části stránky galerie prostředí PowerShell místo registrace.
Kliknutím na na své uživatelské jméno se dostanete na stránku Můj účet, kde zjistíte, klíč rozhraní API.

Poznámka: Klíč rozhraní API musí být považované bezpečně jako přihlašovací jméno a heslo.
Pomocí tohoto klíče nebo nikdo jiný, můžete aktualizovat všechny položky, které vlastníte v galerii prostředí PowerShell.
Doporučujeme aktualizovat klíč pravidelně, což lze provést pomocí resetovat klíče na stránce Můj účet.

## <a name="required-metadata-for-items-published-to-the-powershell-gallery"></a>Požadovaná Metadata pro položky, které jsou publikovány do Galerie prostředí PowerShell

Galerie prostředí PowerShell poskytuje informace o Galerie uživatelé čerpají z pole metadat, které jsou zahrnuty do skriptu nebo modul manifestu.
Vytvoření nebo úprava položky pro publikaci do Galerie prostředí PowerShell má malého požadavků pro informací získaných v manifestu položky.
Důrazně doporučujeme, abyste si prošli části Metadata položky [pokyny pro publikování](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/psgallery-PublishingGuidelines) se dozvíte, jak poskytnout uživatelům informace o osvědčených s položkami.

[New-ModuleManifest](https://msdn.microsoft.com/en-us/powershell/gallery/psget/module/ModuleManifest-Reference) a [New-ScriptFileInfo](https://msdn.microsoft.com/en-us/powershell/gallery/psget/script/psget_new-scriptfileinfo) rutiny manifestu šablony pro vytvoření, se zástupnými symboly pro všechny elementy manifestu.

Jak manifesty mají dvě části, které jsou důležité pro publikování, primární klíč dat a PSData oblasti PrivateData primární klíče data v manifestu modulu prostředí PowerShell je všechno mimo části PrivateData.
Sadě primárních klíčů je vázaný na verzi prostředí PowerShell v použití a není definovaná nejsou podporovány.
PrivateData podporuje přidávání nových klíčů, tak, aby elementy, které jsou specifické pro galerii prostředí PowerShell v PSData.


Manifestu prvky, které jsou důležité vyplnit pro položku, kterou publikujete do Galerie prostředí PowerShell jsou:

- Skript nebo název modulu - těch, které se mají vykreslovat od názvů. PS1 pro skript, nebo. PSD1 pro modul.
- Verze – jedná se o požadované primární klíč, formát by měl postupovat podle pokynů SemVer (podrobnosti najdete v části osvědčené postupy)
- Autor – to je požadovaná primární klíč a obsahuje název, který má být přidružená k položce (viz autoři a vlastníky, níže)
- Popis – to je požadovaná primární klíč, použít k stručně popisují, co dělají tuto položku a případné požadavky pro použití
- ProjectURI – to je důrazně ho doporučujeme pole URI v PSData, který obsahuje odkaz na úložiště Github nebo podobné umístění, kde můžete udělat vývoj položky

Autoři a Galerie prostředí PowerShell vlastníci položky jsou související koncepty, ale vždy neodpovídají.
Vlastníci položky jsou uživatelé s účty Galerie prostředí PowerShell, které mají oprávnění k udržování položce. Může mít mnoho vlastníky, kdo může aktualizovat jakoukoli položku.
Vlastník je k dispozici pouze z Galerie prostředí PowerShell a dojde ke ztrátě, pokud bude položka zkopírována z jednoho systému do jiného.
Autor je řetězec, který je integrovaný do manifestu dat tak, aby byl vždy část položky.
Doporučení pro položky z produktů společnosti Microsoft jsou:

- Máte několik vlastníky s alespoň jedním se název týmu, který vytvoří položku;
- Máte Autor být název dobře známé team (například týmu Azure SDK) nebo Microsoft Corporation.


## <a name="pre-validate-your-item"></a>Předběžné ověření vaší položky

Existuje několik nástrojů, které potřebujete ke spouštění kódu před publikováním vaší položky do Galerie prostředí PowerShell:

- [Analyzátor skriptu prostředí PowerShell](https://www.powershellgallery.com/packages/PSScriptAnalyzer/), což je v galerii prostředí PowerShell
- Pro moduly, Test-ModuleManifest, která je součástí prostředí PowerShell
- Pro skripty, testovací ScriptFileInfo, který se dodává s prostředí PowerShell Get

[Analyzátor skriptu prostředí PowerShell](https://www.powershellgallery.com/packages/PSScriptAnalyzer/) je nástroj pro analýzu statické kódu, který vyhledá kódu tak, aby byl splňuje základní prostředí PowerShell pokyny pro kódování. Tento nástroj se identifikovat běžné a důležité problémy ve vašem kódu a by měl být spouštěn pravidelně během vývoje, které vám pomohou vaše položky připravena k publikování.
Analyzátor skriptu prostředí PowerShell vám poskytne seznam jako chyby, upozornění a informace o zjištěné potíže.
Před publikováním do Galerie prostředí PowerShell, je nutné vyřešit všechny chyby. Upozornění potřebovat mají být zkontrolovány a mělo by se řešit většinu.
Analyzátor skriptu prostředí PowerShell je spuštěn pokaždé, když je položka publikovaných nebo aktualizovány v galerii prostředí PowerShell.
Galerie provozní tým vás bude kontaktovat položky vlastníkům chyby adres, které se nacházejí.

Pokud manifestu informace ve vaší položky nelze číst z infrastruktury pro galerii prostředí PowerShell, nebudete moci publikovat.
[Test ModuleManifest](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/test-modulemanifest) zachytí běžné problémy, které by způsobily modul není možné používat při instalaci. Musí být spuštěn pro každý modul před publikováním do Galerie prostředí PowerShell.

Podobně [Test ScriptFileInfo](https://msdn.microsoft.com/en-us/powershell/gallery/psget/script/psget_test-scriptfileinfo) ověří metadata ve skriptu a musí být spuštěn na každý skript (publikované odděleně od modulu) před publikováním do Galerie prostředí Powershell.


## <a name="publishing-items"></a>Publikování položky

Je nutné použít [publikovat skriptu](https://msdn.microsoft.com/en-us/powershell/gallery/psget/script/psget_publish-script) nebo [publikovat modulu](https://msdn.microsoft.com/en-us/powershell/gallery/psget/module/psget_publish-module) publikování položky galerie prostředí PowerShell.
Tyto příkazy, které oba vyžadují

- Cesta pro položku, kterou budete publikovat. Pro modul použijte složku s názvem pro modul. Pokud jste určili složky, která obsahuje více verzí stejného modulu, musíte zadat RequiredVersion.
- Klíč rozhraní API Nuget. Toto je klíč rozhraní API najít na stránce Můj účet v galerii prostředí PowerShell.

Většinu dalších možností v příkazovém řádku musí být v manifestu data pro položku, kterou publikujete, proto by nemělo třeba je zadat v příkazu.

Abyste se vyhnuli chybám, důrazně doporučujeme vyzkoušet příkazů pomocí - Whatif-Verbose, před publikováním.
Tato akce uloží mnoho času, protože pokaždé, když publikujete do Galerie prostředí PowerShell, je nutné aktualizovat číslo verze v oddílu manifestu sady položky.

Příklady by: ' Publish-Module-cestu ". \MyModule" - RequiredVersion "0.0.1" - NugetAPIKey "GUID" - Whatif-podrobné ' ' publikovat skriptu-cestu ".\MyScriptFile.PS1" - NugetAPIKey "GUID" - Whatif-podrobné '

Pečlivě zkontrolujte výstup a pokud se žádné chyby nebo upozornění, opakujte příkaz bez - Whatif.

Všechny položky, které jsou publikovány do Galerie prostředí PowerShell bude hledat viry a analyzuje pomocí Analyzéru skript prostředí PowerShell.
Všechny problémy, které mohou nastat v té době zašle zpět k vydavateli pro překlad.

Po publikování položky galerie prostředí PowerShell musíte sledovat zpětná vazba týkající se vaší položky.

- Ujistěte se, sledovat e-mailovou adresu, přidružené k účtu použít k publikování.
Uživatelé a provozní Galerie prostředí PowerShell tým bude poskytovat zpětnou vazbu prostřednictvím tohoto účtu, včetně problémů z PSSA nebo antivirovou kontrolu.
Pokud není platná e-mailový účet, nebo pokud vážný problém nahlásí na účet a levé straně nepřeložené po dlouhou dobu, položky lze považovat za opuštění a bude odebrána z Galerie prostředí PowerShell, jak je popsáno v našem [podmínky použití](https://www.powershellgallery.com/policies/Terms).
- Doporučujeme, aby že se přihlásíte k odběru komentáře pro každou položku Galerie prostředí PowerShell, které můžete publikovat.
To umožňuje se upozornění, že každý, kdo komentování položek v galerii prostředí PowerShell.
Tato položka je nepovinná, protože vyžaduje vytvoření účtu s LiveFyre.