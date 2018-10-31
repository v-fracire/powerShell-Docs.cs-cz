---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Vytvoření a publikování položky
ms.openlocfilehash: ced892b558b81c3ef9575b5a01e74932515b412a
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004011"
---
# <a name="creating-and-publishing-an-item"></a>Vytvoření a publikování položky

Galerie prostředí PowerShell je místem, kde můžete publikovat a sdílet stabilní moduly Powershellu, skripty a prostředky DSC s širší komunity uživatelské prostředí PowerShell.

Tento článek se týká mechanismy a důležité kroky pro přípravu skriptu nebo modulu a publikujete ji v galerii prostředí PowerShell.
Důrazně doporučujeme, abyste se seznámili [pokyny pro publikování](/powershell/gallery/concepts/publishing-guidelines) pochopit, jak zajistit, že položky publikujete větší míře přijme uživatelé Galerie prostředí PowerShell.

Jsou minimální požadavky nutné k publikujte položku v galerii prostředí PowerShell:

- Mít účet Galerie prostředí PowerShell a klíč rozhraní API s ním spojená.
- Ujistěte se, že se vyžaduje Metadata položky
- Ujistěte se, že je připravená k publikování vaší položky pomocí nástrojů pro předběžné ověření
- Publikujte položku v galerii prostředí PowerShell pomocí příkazu Publish-Module a Publish-Script
- Reagování na dotazy nebo pochybnostmi k vaší položce

Galerie prostředí PowerShell přijímá moduly Powershellu a skripty prostředí PowerShell.
Když budeme odkazovat na skripty, myslíme skript prostředí PowerShell, který je jediný soubor a není součástí větší modulu.

## <a name="powershell-gallery-account-and-api-key"></a>Galerie prostředí PowerShell účtu a klíč rozhraní API

Zobrazit [vytvořením účtu Galerie prostředí PowerShell](/powershell/gallery/how-to/publishing-packages/creating-an-account) postup nastavení účtu Galerie prostředí PowerShell.

Po vytvoření účtu můžete získat klíč rozhraní API, které jsou potřebné k publikování položky.
Po přihlášení pomocí účtu své uživatelské jméno se zobrazí v horní části stránky galerie prostředí PowerShell místo registrace.
Kliknutím na své uživatelské jméno se dostanete na stránku Můj účet, kde najdete klíč rozhraní API.

Poznámka: Klíč rozhraní API musí být považované bezpečně jako přihlašovací jméno a heslo.
S tímto klíčem vy nebo někdo jiný, můžete aktualizovat všechny položky, které vlastníte v galerii prostředí PowerShell.
Doporučujeme aktualizovat klíče pravidelně, což lze provést pomocí obnovení klíče na stránce Můj účet.

## <a name="required-metadata-for-items-published-to-the-powershell-gallery"></a>Požadovaná Metadata pro položky publikována do Galerie prostředí PowerShell

Galerie prostředí PowerShell poskytuje informace o galerii uživatelů z pole metadat, které jsou součástí manifestu skriptu nebo modulu.
Vytvoření nebo úprava položky pro publikování v galerii prostředí PowerShell má malou sadu požadavků na informace v manifestu položky.
Důrazně doporučujeme, abyste si část Metadata položky [pokyny pro publikování](/powershell/gallery/concepts/publishing-guidelines) postup, jak můžete uživatelům poskytnout informace o osvědčených s položkami.

[New-ModuleManifest](/powershell/module/microsoft.powershell.core/new-modulemanifest) a [New-ScriptFileInfo](/powershell/module/PowerShellGet/New-ScriptFileInfo) rutin vytvoří šablonu manifestu, se zástupnými symboly pro všechny elementy manifestu.

Jak manifesty dva oddíly, které jsou důležité pro publikování, oblasti dat primární klíč a PSData PrivateData data primárního klíče v manifestu modulu prostředí PowerShell je všechno, co mimo PrivateData oddílu.
Množině primárních klíčů je vázané na verze Powershellu používá a nedefinované nejsou podporovány.
PrivateData podporuje přidávání nových klíčů, tak, aby elementy, které jsou specifické pro galerii prostředí PowerShell v PSData.


Jsou manifestu prvky, které jsou nejdůležitější vyplnit pro položku, kterou budete publikovat v galerii prostředí PowerShell:

- Skript nebo název modulu – ty jsou vykreslovány vedle od názvů. PS1 pro skript, nebo. PSD1 pro modul.
- Verze – to je požadovaná primární klíč, formát by měl postupovat podle pokynů SemVer (podrobnosti naleznete v tématu Doporučené postupy)
- Autor – to je požadovaná primární klíč a obsahuje název, který má být přidružená k položce (viz autoři a vlastníci níže)
- Popis – to je požadovaná primární klíč, umožňuje stručně popisují, co dělá tuto položku a případné požadavky pro použití
- ProjectURI – to je důrazně ho doporučujeme pole identifikátoru URI v PSData, který poskytuje odkaz na úložiště Github nebo podobně jako umístění, kde provádíte vývoj na položku

Autoři a vlastníci Galerie prostředí PowerShell položky jsou souvisejí, ale vždy neshodují.
Vlastníci položky jsou uživatelé s účty Galerie prostředí PowerShell, které mají oprávnění spravovat položky. Může existovat mnoho vlastníků, kdo může aktualizovat všechny položky.
Vlastník je k dispozici pouze z Galerie prostředí PowerShell a dojde ke ztrátě, pokud se položka zkopíruje z jednoho systému do druhého.
Autorem je řetězec, který je integrovaný do manifestu data tak, aby byl vždy část položky.
Doporučení pro položky z produktů společnosti Microsoft jsou:

- Máte více vlastníkům, s alespoň jedním se název týmu, který vytvoří položku;
- Máte Autor být název dobře známé tým (třeba Azure SDK týmu) nebo Microsoft Corporation.


## <a name="pre-validate-your-item"></a>Předběžně ověřit vaši položku

Existuje několik nástrojů, které potřebujete ke spuštění kódu před publikováním vaši položku v galerii prostředí PowerShell:

- [Analyzátor skript prostředí PowerShell](https://www.powershellgallery.com/packages/PSScriptAnalyzer/), což je v galerii prostředí PowerShell
- Pro moduly, Test-ModuleManifest, která je součástí prostředí PowerShell
- Pro skripty, Test-ScriptFileInfo, která je součástí prostředí PowerShell Get

[Analyzátor skript prostředí PowerShell](https://www.powershellgallery.com/packages/PSScriptAnalyzer/) je nástroj pro analýzu statického kódu, která bude skenovat tak, aby byl váš kód splňuje základní Powershellu pokynů pro kódování. Tento nástroj bude identifikovat běžné a důležité problémy ve vašem kódu a by se měl spustit pravidelně během vývoje, které vám pomůžou získat připraveni publikovat vaši položku.
Analyzátor skript prostředí PowerShell poskytne seznam problémů, které jsou identifikovány jako chyby, upozornění a informace.
Před publikováním v galerii prostředí PowerShell, musí se vyřešit všechny chyby. Upozornění musí být zkontrolovány a mělo by se řešit většinu.
Analyzátor skript prostředí PowerShell se spustí pokaždé, když položka publikována nebo aktualizována v galerii prostředí PowerShell.
Galerie provozní tým bude kontaktovat vlastníků položky pro chyby adres, které se nacházejí.

Pokud nejde přečíst informace o manifestu v vaši položku Galerie prostředí PowerShell infrastruktura, nebude možné publikovat.
[Test-ModuleManifest](/powershell/module/microsoft.powershell.core/test-modulemanifest) zachytí běžné problémy, které by mohly způsobit modul není možné použít při instalaci. Musí se spustit pro každý modul před publikováním v galerii prostředí PowerShell.

Obdobně [testovací ScriptFileInfo](/powershell/module/PowerShellGet/test-scriptfileinfo) ověří metadata ve skriptu a je třeba spustit na každý skript (publikované odděleně od modul) před publikováním v galerii prostředí Powershell.


## <a name="publishing-items"></a>Publikování položek

Je nutné použít [Publish-Script](/powershell/module/PowerShellGet/publish-script) nebo [Publish-Module](/powershell/module/PowerShellGet/publish-module) publikování položek v galerii prostředí PowerShell.
Tyto příkazy, které vyžadují

- Cesta k položce, kterou budete publikovat. Pro modul použijte složku pro modul. Pokud chcete zadat složku, která obsahuje více verzí stejného modulu, musíte zadat RequiredVersion.
- Klíč rozhraní API Nuget. Toto je klíč rozhraní API, který najdete na stránce Můj účet na galerii prostředí PowerShell.

Většinu dalších možností v příkazovém řádku musí být v manifestu data pro položku, kterou publikujete, takže by neměl muset zadat v příkazu.

Aby nedocházelo k chybám, důrazně doporučujeme, zkuste příkazy pomocí - Whatif-Verbose, před publikováním.
To vám ušetří docela dlouho, protože pokaždé, když publikujete v galerii prostředí PowerShell, je nutné aktualizovat číslo verze do oddílu manifestu položky.

Příklady by: "Publish-Module – cestu". \MyModule "- RequiredVersion"0.0.1"- NugetAPIKey"GUID"- Whatif – podrobné" "Publish-Script – cesty".\MyScriptFile.PS1"- NugetAPIKey"GUID"- Whatif-Verbose"

Pečlivě zkontrolujte výstup a pokud se zobrazí, žádné chyby nebo upozornění, opakujte příkaz bez - Whatif.

Všechny položky, které se publikují v galerii prostředí PowerShell budou vyhledány viry a se dají analyzovat pomocí analyzátoru skriptu prostředí PowerShell.
Všechny problémy, které vznikají v tu chvíli se odešlou zpět k vydavateli řešení.

Po publikování položky v galerii prostředí PowerShell, je potřeba sledovat názory na vaši položku.

- Ujistěte se, sledovat e-mailová adresa přidružená k účtu k publikování.
Uživatelé a provozní Galerie prostředí PowerShell tým poskytne zpětné vazby na tento účet, včetně problémů z PSSA nebo antivirovou kontrolu.
Pokud není platná e-mailový účet, nebo pokud závažných problémech jsou hlášeny k účtu a vlevo nevyřešené po dlouhou dobu, položky lze považovat za opuštěných a bude odebrána z Galerie prostředí PowerShell, jak je popsáno v našem [Terms of Use](https://www.powershellgallery.com/policies/Terms).
- Doporučujeme, abyste že se přihlásíte k odběru komentáře pro každou položku Galerie prostředí PowerShell, kterou publikujete.
To umožňuje vás upozorní, když každý komentáře na položky v galerii prostředí PowerShell.
Tato položka je nepovinná, protože vyžaduje vytvoření účtu se společností LiveFyre.
