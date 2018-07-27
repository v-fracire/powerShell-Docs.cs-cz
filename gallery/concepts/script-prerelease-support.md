---
ms.date: 10/17/2017
contributor: keithb
keywords: Galerie prostředí powershell, rutina, psget
title: Předběžné verze skriptů
ms.openlocfilehash: 14ae1968e5ee73260b6eae05b11185069d047e93
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268462"
---
# <a name="prerelease-versions-of-scripts"></a>Předběžné verze skriptů

Od verze 1.6.0, Správce balíčků PowerShellGet a Galerie prostředí PowerShell poskytuje podporu pro označování verze větší než 1.0.0 jako zkušební verze. Před tato funkce předběžné verze položky byly omezeny s tím, že verze počínaje 0. Cílem těchto funkcí je poskytují větší podporu pro [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) konvence správy verzí bez narušení zpětnou kompatibilitu s verzí Powershellu 3 a vyšší nebo stávající verze Správce balíčků PowerShellGet. Toto téma se zaměřuje na funkce specifické pro skript. Ekvivalentní funkce pro moduly jsou [zkušební verze modulu](module-prerelease-support.md) tématu. Pomocí těchto funkcí, vydavatele můžete identifikovat skript jako verze 2.5.0-alpha a novější verze produkční prostředí 2.5.0, který nahrazuje tuto předprodejní verzi.

Na vysoké úrovni funkce předběžné verze skriptu patří:

- Přidání přípony PrereleaseString řetězec verze v manifestu skriptu. Při publikování skripty v galerii prostředí PowerShell tato data jsou extrahovány z manifestu a slouží k identifikaci předběžné verze položky.
- Získání položky předběžné verze vyžaduje přidání příznak - AllowPrerelease do příkazů PowerShellGet Find-Script instalační skript, skript pro aktualizaci a Save-Script. Pokud se nezadá příznak, nezobrazí se předběžné verze položky.
- Verze skriptu zobrazí Find-Script, Get-InstalledScript a v galerii prostředí PowerShell se zobrazí s PrereleaseString, stejně jako v 2.5.0-alpha.

Podrobnosti o funkcích jsou uvedené níže.

## <a name="identifying-a-script-version-as-a-prerelease"></a>Určení verze skriptu jako zkušební verze

Podpora Správce balíčků PowerShellGet pro předběžné verze je snazší pro skripty než moduly. Skript správy verzí je podporována pouze PowerShellGet, takže nejsou žádné problémy s kompatibilitou způsobila přidáním předběžné verze řetězce. K identifikaci skript v galerii prostředí PowerShell jako zkušební verze, přidáte příponu předběžné verze správně formátovaný řetězec ve skriptu s metadaty.

Vzorový oddíl manifestu skript s předběžnou verzi by vypadat nějak takto:

```powershell
<#PSScriptInfo

.VERSION 3.2.1-alpha12

.GUID

...

#>
```

Pokud chcete použít příponu předběžné verze, řetězec verze musí splňovat následující požadavky:

- Příponu předběžné verze jde zadat jenom když je verze 3 segmenty Major.Minor.Build.
  Ten je v souladu s SemVer v1.0.0
- Předběžné verze přípona je řetězec, který začíná spojovníkem a může obsahovat alfanumerické znaky ASCII [0-9A-Za - z-]
- Jsou podporovány pouze řetězce předběžnou verzi v1.0.0 SemVer v tuto chvíli tak příponu předběžné verze **nesmí** obsahovat buď období nebo + [. +], které jsou povoleny v SemVer 2.0
- Příklady podporovaných řetězců PrereleaseString:-alfa, - α1,-BETA, - update20171020

### <a name="prerelease-versioning-impact-on-sort-order-and-installation-folders"></a>Předběžné verze správy verzí dopad na složky instalace a pořadí řazení

Pořadí řazení se změní při používání předběžné verze, což je důležité při publikování do Galerie prostředí PowerShell, a při instalaci skriptů pomocí příkazů PowerShellGet. Pokud dva skripty verze s číslem verze neexistuje, pořadí řazení je podle následující spojovník část řetězce. Ano 2.5.0-alpha verze je menší než 2.5.0-beta, což je míň než 2.5.0-gamma. Pokud dva skripty mají stejné číslo verze a pouze jeden má PrereleaseString, skript **bez** příponu předběžné verze se předpokládá se, že verze připravené pro produkční prostředí a budou seřazeny jako větší než zkušební verze verze. Jako příklad, když porovnání uvolní 2.5.0 a 2.5.0-beta, 2.5.0 verzi se budou považovat za větší z nich.

Při publikování do Galerie prostředí PowerShell, ve výchozím nastavení verzi publikován skriptu musí mít s vyšší verzí, než všechny dříve publikované verzi, která je v galerii prostředí PowerShell. Vydavatel může aktualizovat verzi 2.5.0-alpha 2.5.0-beta nebo s 2.5.0 (s příponou žádné předběžné verze).

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a>Hledání a získávání předběžnou verzi položky pomocí příkazů PowerShellGet

Práce s předběžnou verzi položky pomocí Správce balíčků PowerShellGet Find-Script, Install-Script aktualizace skriptu, a příkazy Save-Script vyžaduje přidání příznaku - AllowPrerelease. Pokud - AllowPrerelease není zadána, předběžné verze položky budou zahrnuty v případě, že jsou k dispozici. Pokud se nezadá příznak - AllowPrerelease, nezobrazí se předběžné verze položky.

Jedinou výjimkou tohoto v příkazy skriptu PowerShellGet jsou Get-InstalledScript a někdy se skript pro odinstalaci.

- Get-InstalledScript vždy automaticky zobrazí informace o předběžnou verzi v řetězci verze pokud je k dispozici.
- Odinstalovat skriptu bude ve výchozím nastavení odinstalace nejnovější verzi skriptu, pokud **žádná verze** je zadán. Aby nedošlo ke změně chování. Nicméně pokud předprodejní verze určena pomocí `-RequiredVersion`, `-AllowPrerelease` se bude vyžadovat.

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
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...ets.FindPackage:FindPackage)[Find-Package], Exception
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

Odinstalovat skript odebere aktuální verzi skriptu, pokud není zadán - RequiredVersion.
Pokud je zadán - RequiredVersion a je zkušební verze, - AllowPrerelease musí přidat k příkazu.

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

## <a name="more-details"></a>Další podrobnosti

- [Verze předběžnou verzi modulu](module-prerelease-support.md)
- [Find-script](/powershell/module/powershellget/find-script)
- [Instalační skript](/powershell/module/powershellget/install-script)
- [Save-script](/powershell/module/powershellget/save-script)
- [Skript pro aktualizaci](/powershell/module/powershellget/update-script)
- [Get-Installedscript](/powershell/module/powershellget/get-installedscript)
- [Odinstalace script](/powershell/module/powershellget/uninstall-script)