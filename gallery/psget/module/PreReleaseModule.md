---
ms.date: 09/26/2017
contributor: keithb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: PrereleaseModule
ms.openlocfilehash: 1fc08cbba90e3eb8ca7d280e4d279af1d8aa279f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="prerelease-module-versions"></a>Modul předprodejní verze
Počínaje verzí 1.6.0, PowerShellGet a Galerie prostředí PowerShell poskytuje podporu pro označování příznaky verze větší než 1.0.0 jako zkušební verze. Před touto funkcí předprodejní položky byly omezeny na situaci, kdy verze počínaje 0. Cílem těchto funkcí je poskytují větší podporu pro [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) konvence Správa verzí, aniž by vás zpětnou kompatibilitu s verzemi 3 a výše uvedené nebo existující verze prostředí PowerShell služby PowerShellGet. Toto téma se zaměřuje na funkce specifické pro modul. Ekvivalentní funkce skriptů jsou v [vydanou verzí skripty](../script/PrereleaseScript.md) tématu. Používání těchto funkcí, vydavatelů můžete identifikovat modulu nebo skriptu jako verze 2.5.0-alpha a novější verze na produkční prostředí verzi 2.5.0, která nahrazuje předběžné verze.

Na vysoké úrovni funkce předběžné verze modulu patří:

* Přidání předprodejní řetězec do části PSData manifestu modulu identifikuje modul jako předprodejní verze.
Pokud modul je publikovaná v galerii prostředí PowerShell, tato data jsou extrahovány z manifestu a použít k identifikaci předprodejní položky.
* Získávání předprodejní položky vyžaduje přidání příznak - AllowPrerelease PowerShellGet příkazy najít-Module instalace modulu, aktualizace modulu a uložit modulu.
Pokud není zadán příznak, nebude se zobrazovat předprodejní položky.
* Verze modulu zobrazovat najít-modulu, Get-InstalledModule a v galerii prostředí PowerShell se zobrazí jako jeden řetězec předprodejní řetězcem, který připojí jako 2.5.0-alpha.

Podrobnosti pro funkce, které jsou popsány níže.

Tyto změny neovlivňují podpora verze modulu, který je součástí prostředí PowerShell a jsou kompatibilní s prostředím PowerShell 3.0, 4.0 a 5.

## <a name="identifying-a-module-version-as-a-prerelease"></a>Identifikace verze modulu jako zkušební verze

Podpora PowerShellGet pro předběžné verze vyžaduje použití dvě pole v manifestu modulu:

* Verze modulu zahrnuté v manifestu modulu musí být verze 3 část, pokud předprodejní verze se používá a musí být v souladu s existující verze prostředí PowerShell. Verze formátu by A.B.C, kde A, B a C jsou všechny celá čísla.
* Předběžné verze řetězec je zadáno v manifestu modulu, v části PSData PrivateData.
Podrobné požadavky na předprodejní řetězce jsou níže.

Příklad části modul manifestu, který definuje modul jako zkušební verze by vypadat třeba takto:
```powershell
@{
    ModuleVersion = '2.5.0'
    #---
    PrivateData = @{
        PSData = @{
            Prerelease = 'alpha'
        }
    }
}
```

Podrobné požadavky pro předběžné verze řetězce jsou:

* Předběžné verze řetězec lze zadat pouze pokud verze modulu 3 segmenty pro Major.Minor.Build. To zarovnaná s SemVer v1.0.0.
* Pomlčka je odděleny číslo sestavení a předběžné verze řetězce. Pomlčka může být součástí předběžné verze řetězec jako první znak, pouze.
* Předběžné verze řetězce mohou obsahovat pouze alfanumerické znaky ASCII [0-9A-Za - z –]. Je osvědčeným postupem zahájit zkušební řetězce s alfanumerický znak, jako je jednodušší zjistit, to je předprodejní verze při kontrole seznam položek.
* V tuto chvíli jsou podporovány pouze SemVer v1.0.0 předprodejní řetězce. Předběžné verze řetězec __musí není__ obsahovat buď období nebo + [. +], které jsou povoleny v SemVer 2.0.
* Příklady podporovaných předprodejní řetězec:-alpha, - α1,-BETA, - update20171020

__Předprodejní verze dopad na složky instalace a pořadí řazení__

Pořadí řazení se změní při použití předprodejní verze, což je důležité při publikování do Galerie prostředí PowerShell, a při instalaci modulů pomocí PowerShellGet příkazy.
Pokud předprodejní řetězec je zadán pro dva moduly, pořadí řazení podle části řetězce následující spojovník. Ano 2.5.0-alpha verze je menší než 2.5.0-beta, která je menší než 2.5.0-gamma.
Pokud dva moduly mají stejné verze modulu a jenom jedna má předprodejní řetězec, se předpokládá, že jako verze na produkční prostředí a seřadí jako vyšší verzi než předprodejní verze (která zahrnuje zkušební modul bez předprodejní řetězec řetězec).
Jako příklad, při porovnání uvolní 2.5.0 a 2.5.0-beta, 2.5.0 verze bude považovat za delší než dva.

Při publikování do Galerie prostředí PowerShell, ve výchozím nastavení verzi modulu publikovanému musí mít vyšší verzi než všechny dříve publikované verze, která je v galerii prostředí PowerShell.

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a>Hledání a získávání předprodejní položek pomocí PowerShellGet příkazy

Plánování práce s předprodejní položek pomocí modulu-najít PowerShellGet-Module, instalace modulu, aktualizace, a příkazy Uložit-Module vyžaduje přidání příznak - AllowPrerelease.
Pokud je zadán - AllowPrerelease, předprodejní položky budou zahrnuty, pokud jsou přítomna.
Pokud není zadán příznak - AllowPrerelease, nebude se zobrazovat předprodejní položky.

To v příkazech modulu PowerShellGet jedinou výjimkou jsou Get-InstalledModule a někdy modulem odinstalovat.

* Get-InstalledModule vždy se automaticky zobrazí předběžné informace v řetězec verze pro moduly.
* Odinstalujte modul bude ve výchozím nastavení nejnovější verzi odinstalujte modul, pokud __žádná verze__ je zadán. Daná chování se nezměnilo. Ale pokud předprodejní verze je zadán pomocí - RequiredVersion, - AllowPrerelease se bude vyžadovat.

## <a name="examples"></a>Příklady
```powershell
# Assume the PowerShell Gallery has TestPackage module versions 1.8.0 and 1.9.0-alpha. If -AllowPrerelease is not specified, only version 1.8.0 will be returned.
C:\windows\system32> find-module TestPackage

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.8.0          TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> find-module TestPackage -AllowPrerelease

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.9.0-alpha    TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

# To install a prerelease, always specify -AllowPrerelease. Specifying a prerelease version string is not sufficient.

C:\windows\system32> Install-module TestPackage -RequiredVersion 1.9.0-alpha
PackageManagement\Find-Package : No match was found for the specified search criteria and module name 'TestPackage'.
Try Get-PSRepository to see all available registered module repositories.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.6.0\PSModule.psm1:1455 char:3
+         PackageManagement\Find-Package @PSBoundParameters | Microsoft ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...ets.FindPackage:FindPackage) [Find-Package], Exceptio
   n
    + FullyQualifiedErrorId : NoMatchFoundForCriteria,Microsoft.PowerShell.PackageManagement.Cmdlets.FindPackage

# The previous command failed because -AllowPrerelease was not specified.
# Adding -AllowPrerelease will result in success.

C:\windows\system32> Install-module TestPackage -RequiredVersion 1.9.0-alpha -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-alpha     TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

```

Souběžně sdílená instalace verze modulu, které se liší pouze z důvodu předběžné verze zadané není podporována.
Při instalaci modulu pomocí PowerShellGet, jsou různé verze stejného modulu nainstalované-souběžného vytvořením název složky pomocí verze modulu.
Verze modulu, bez předprodejní řetězec se používá v názvu složky.
Pokud uživatel nainstaluje verzi 2.5.0-alpha MyModule, nainstaluje se do složky MyModule\2.5.0.
Pokud uživatel potom nainstaluje 2.5.0-beta, bude verze 2.5.0-beta __přečerpání zápisu__ obsah složky MyModule\2.5.0.
Jednou z výhod tohoto přístupu je, že není nutné provést odinstalaci Tuto předprodejní verzi po instalaci verze produkční prostředí.
Následující příklad ukazuje, co můžete očekávat:


``` powershell
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-alpha     TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> find-module TestPackage -AllowPrerelease

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.9.0-beta     TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> Update-Module TestPackage -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-beta      TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

```

Odinstalujte modul odeberete nejnovější verzi modulu, pokud není zadáno - RequiredVersion.
Pokud - RequiredVersion byl zadán a je předběžné verze, - AllowPrerelease je nutné přidat do příkazu.

``` powershell
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
2.0.0-alpha1    TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.9.0-beta      TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> Uninstall-Module TestPackage -RequiredVersion 1.9.0-beta
Uninstall-Module : The '-AllowPrerelease' parameter must be specified when using the Prerelease string in
MinimumVersion, MaximumVersion, or RequiredVersion.
At line:1 char:1
+ Unnstall-Module TestPackage -RequiredVersion 1.9.0-beta
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Uninstall-Module], ArgumentException
    + FullyQualifiedErrorId : AllowPrereleaseRequiredToUsePrereleaseStringInVersion,Uninnstall-Module



C:\windows\system32> Uninstall-Module TestPackage -RequiredVersion 1.9.0-beta -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
2.0.0-alpha1    TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> Uninstall-Module TestPackage
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...


```



## <a name="more-details"></a>Další informace
### <a name="prerelease-script-versionsscriptprereleasescriptmd"></a>[Skript předprodejní verze](../script/PrereleaseScript.md)
### <a name="find-modulepsgetfind-modulemd"></a>[Najít – modul](./psget_find-module.md)
### <a name="install-modulepsgetinstall-modulemd"></a>[Instalace modulu](./psget_install-module.md)
### <a name="save-modulepsgetsave-modulemd"></a>[Save-Module](./psget_save-module.md)
### <a name="update-modulepsgetupdate-modulemd"></a>[Update-Module](./psget_update-module.md)
### <a name="get-installedmodulepsgetget-installedmodulemd"></a>[Get-InstalledModule](./psget_get-installedmodule.md)
### <a name="uninstall-modulepsgetuninstall-modulemd"></a>[Odinstalujte modul](./psget_uninstall-module.md)