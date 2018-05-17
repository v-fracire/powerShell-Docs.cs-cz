---
ms.date: 10/17/2017
contributor: keithb
keywords: Galerie prostředí powershell, rutiny, psget
title: Předprodejní verze skriptů
ms.openlocfilehash: 5b93da418b836d537491d3f1e4e29fa2e61f2f77
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="prerelease-versions-of-scripts"></a>Předprodejní verze skriptů

Počínaje verzí 1.6.0, PowerShellGet a Galerie prostředí PowerShell poskytuje podporu pro označování příznaky verze větší než 1.0.0 jako zkušební verze. Před touto funkcí předprodejní položky byly omezeny na situaci, kdy verze počínaje 0. Cílem těchto funkcí je poskytují větší podporu pro [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) konvence Správa verzí, aniž by vás zpětnou kompatibilitu s verzemi 3 a výše uvedené nebo existující verze prostředí PowerShell služby PowerShellGet. Toto téma se zaměřuje na funkce specifické pro skript. Ekvivalentní funkce pro moduly jsou v [předběžné verze modulu verze](module-prerelease-support.md) tématu. Používání těchto funkcí, vydavatelů můžete identifikovat skript jako verze 2.5.0-alpha a novější verze na produkční prostředí verzi 2.5.0, která nahrazuje předběžné verze.

Na vysoké úrovni funkce předběžné verze skriptu patří:

- Přidání přípony PrereleaseString na řetězec verze ve skriptu manifest. Pokud skripty je publikovaná v galerii prostředí PowerShell, tato data jsou extrahovány z manifestu a použít k identifikaci předprodejní položky.
- Získávání předprodejní položky vyžaduje přidání příznak - AllowPrerelease PowerShellGet příkazy skriptu najít instalační skript, skript aktualizace a uložit skript. Pokud není zadán příznak, nebude se zobrazovat předprodejní položky.
- Verze skriptu zobrazí najít-skript, Get-InstalledScript a v galerii prostředí PowerShell se zobrazí PrereleaseString, stejně jako 2.5.0-alpha.

Podrobnosti pro funkce, které jsou popsány níže.

## <a name="identifying-a-script-version-as-a-prerelease"></a>Identifikace verze skriptu jako zkušební verze

Podpora PowerShellGet pro předběžné verze je snazší pro skripty než moduly. Správa verzí skriptu je podporována pouze PowerShellGet, proto nejsou žádné problémy s kompatibilitou způsobené přidání předprodejní řetězec. K identifikaci skript v galerii prostředí PowerShell jako zkušební verze, přidejte příponu předprodejní na řetězec správně naformátován verzi v metadatech skriptu.

Na příkladu část skriptu manifest s předprodejní verze by vypadat následovně:

```powershell
<#PSScriptInfo

.VERSION 3.2.1-alpha12

.GUID

...

#>

```

Pokud chcete používat příponu předprodejní, řetězec verze musí splňovat následující požadavky:

- Předběžné verze příponu lze zadat pouze pokud je verze 3 segmenty pro Major.Minor.Build.
  To zarovnaná s SemVer v1.0.0
- Předběžné verze přípona je řetězec, který začíná pomlčka a může obsahovat alfanumerické znaky ASCII [0-9A-Za - z –]
- Pouze SemVer v1.0.0 předprodejní řetězce jsou podporovány v tuto chvíli tak předprodejní přípona __musí není__ obsahovat buď období nebo + [. +], které jsou povoleny v SemVer 2.0
- Příklady podporovaných řetězců PrereleaseString:-alpha, - α1,-BETA, - update20171020

__Předprodejní verze dopad na složky instalace a pořadí řazení__

Pořadí řazení se změní při použití předprodejní verze, což je důležité při publikování do Galerie prostředí PowerShell, a při instalaci pomocí příkazů PowerShellGet skripty. Pokud dvě verze číslo verze skriptů existují, pořadí řazení podle části řetězce následující spojovník. Ano 2.5.0-alpha verze je menší než 2.5.0-beta, která je menší než 2.5.0-gamma. Pokud dva skripty mít stejné číslo verze a jenom jedna má PrereleaseString, skript __bez__ předprodejní příponu se předpokládá, že jako verze na produkční prostředí a seřadí jako vyšší verzi než zkušební verze. Jako příklad, při porovnání uvolní 2.5.0 a 2.5.0-beta, 2.5.0 verze bude považovat za delší než dva.

Při publikování do Galerie prostředí PowerShell, ve výchozím nastavení verze skriptu publikovanému musí mít vyšší verzi než všechny dříve publikované verze, která je v galerii prostředí PowerShell. Vydavatelem může aktualizovat verzi 2.5.0-alpha 2.5.0-beta nebo s 2.5.0 (s příponou žádné předprodejní).

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a>Hledání a získávání předprodejní položek pomocí PowerShellGet příkazy

Plánování práce s předprodejní položek pomocí skript-PowerShellGet najít skriptu, instalační skript, aktualizace, a příkazy skriptu uložit vyžaduje přidání příznak - AllowPrerelease. Pokud je zadán - AllowPrerelease, předprodejní položky budou zahrnuty, pokud jsou přítomna. Pokud není zadán příznak - AllowPrerelease, nebude se zobrazovat předprodejní položky.

To v příkazy skriptu PowerShellGet jedinou výjimkou jsou Get-InstalledScript a někdy s odinstalační skript.

- Get-InstalledScript vždy se automaticky zobrazí předběžné informace v řetězec verze pokud je k dispozici.
- Odinstalujte skript bude ve výchozím nastavení nejnovější verzi odinstalujte skriptu, pokud __žádná verze__ je zadán. Daná chování se nezměnilo. Ale pokud předprodejní verze je zadán pomocí - RequiredVersion, - AllowPrerelease se bude vyžadovat.

## <a name="examples"></a>Příklady

```powershell
# Assume the PowerShell Gallery has TestPackage versions 1.8.0 and 1.9.0-alpha.
# If -AllowPrerelease is not specified, only version 1.8.0 will be returned.
C:\windows\system32> Find-Script TestPackage

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.8.0          TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> Find-Script TestPackage -AllowPrerelease

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.9.0-alpha    TestPackage                         PSGallery            Package used to validate changes to PowerShe...

# To install a prerelease, you must specify -AllowPrerelease. Specifying a prerelease version string is not sufficient.

C:\windows\system32> Install-Script TestPackage -RequiredVersion 1.9.0-alpha
PackageManagement\Find-Package : No match was found for the specified search criteria and script name 'TestPackage'.
Try Get-PSRepository to see all available registered script repositories.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.6.0\PSModule.psm1:1455 char:3
+         PackageManagement\Find-Package @PSBoundParameters | Microsoft ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...ets.FindPackage:FindPackage) [Find-Package], Exceptio
   n
    + FullyQualifiedErrorId : NoMatchFoundForCriteria,Microsoft.PowerShell.PackageManagement.Cmdlets.FindPackage

# The previous command failed because -AllowPrerelease was not specified.
# Adding -AllowPrerelease will result in success.

C:\windows\system32> Install-Script TestPackage -RequiredVersion 1.9.0-alpha -AllowPrerelease
C:\windows\system32> Get-InstalledScript TestPackage

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-alpha     TestPackage                         PSGallery            Package used to validate changes to PowerShe...

# Note that Get-InstalledScript shows the prerelease version.
# If -RequiredVersion is not specified, all installed scripts will be displayed by Get-InstalledScript
```

Odinstalujte skriptu odebere aktuální verze skriptu, pokud není zadáno - RequiredVersion.
Pokud - RequiredVersion byl zadán a je předběžné verze, - AllowPrerelease je nutné přidat do příkazu.

``` powershell
C:\windows\system32> Get-InstalledScript TestPackage

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-alpha     TestPackage                         PSGallery            Package used to validate changes to PowerShe...

C:\windows\system32> Uninstall-Script TestPackage -RequiredVersion 1.9.0-alpha
Uninstall-Script: The '-AllowPrerelease' parameter must be specified when using the Prerelease string in
MinimumVersion, MaximumVersion, or RequiredVersion.
At line:1 char:1
+ Unnstall-Script TestPackage -RequiredVersion 1.9.0-beta
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Uninstall-Script], ArgumentException
    + FullyQualifiedErrorId : AllowPrereleaseRequiredToUsePrereleaseStringInVersion,Uninnstall-script


C:\windows\system32> Uninstall-Script TestPackage -RequiredVersion 1.9.0-alpha -AllowPrerelease
# Since script versions are not installed side-by-side, the above could be simply "Uninstall-Script TestPackage"

C:\windows\system32> Get-Installedscript TestPackage
PackageManagement\Get-Package : No match was found for the specified search criteria and script names 'testpackage'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.5.0.0\PSModule.psm1:4088 char:9
+         PackageManagement\Get-Package @PSBoundParameters | Microsoft. ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...lets.GetPackage:GetPackage) [Get-Package], Exception
    + FullyQualifiedErrorId : NoMatchFound,Microsoft.PowerShell.PackageManagement.Cmdlets.GetPackage
```

## <a name="more-details"></a>Další informace

- [Modul předprodejní verze](module-prerelease-support.md)
- [Najít skriptu](/powershell/module/powershellget/find-script)
- [Instalační skript](/powershell/module/powershellget/install-script)
- [Uložení skriptu](/powershell/module/powershellget/save-script)
- [Skript aktualizace](/powershell/module/powershellget/update-script)
- [Get-Installedscript](/powershell/module/powershellget/get-installedscript)
- [Odinstalujte skriptu](/powershell/module/powershellget/uninstall-script)