---
ms.date: 09/26/2017
contributor: keithb
keywords: Galerie prostředí powershell, rutina, psget
title: Verze předběžnou verzi modulu
ms.openlocfilehash: 9c3ddb623fbcb7f4b3453dd70cdc56a8dc2e9f6a
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268615"
---
# <a name="prerelease-module-versions"></a>Verze předběžnou verzi modulu

Od verze 1.6.0, Správce balíčků PowerShellGet a Galerie prostředí PowerShell poskytuje podporu pro označování verze větší než 1.0.0 jako zkušební verze. Před tato funkce předběžné verze položky byly omezeny s tím, že verze počínaje 0. Cílem těchto funkcí je poskytují větší podporu pro [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) konvence správy verzí bez narušení zpětnou kompatibilitu s verzí Powershellu 3 a vyšší nebo stávající verze Správce balíčků PowerShellGet. Toto téma se zaměřuje na funkce specifické pro modul. Ekvivalentní funkce pro skripty jsou [zkušební verze skriptů](script-prerelease-support.md) tématu. Pomocí těchto funkcí, vydavatelů můžete identifikovat pomocí modulu nebo skriptu jako verze 2.5.0-alpha a novější verze produkční prostředí 2.5.0, který nahrazuje tuto předprodejní verzi.

Na vysoké úrovni zahrnují funkce předběžné verze modulu:

- Přidání předběžné verze řetězce do části PSData manifestu modulu identifikuje jako předprodejní verze modulu. Při publikování modulu v galerii prostředí PowerShell tato data jsou extrahovány z manifestu a slouží k identifikaci předběžné verze položky.
- Získání položky předběžné verze vyžaduje přidání `-AllowPrerelease` příznak příkazů PowerShellGet `Find-Module`, `Install-Module`, `Update-Module`, a `Save-Module`. Pokud se nezadá příznak, nezobrazí se předběžné verze položky.
- Verze modulu zobrazený `Find-Module`, `Get-InstalledModule`a v galerii prostředí PowerShell se zobrazí jako jeden řetězec předprodejní řetězcem, který připojí jako 2.5.0-alpha.

Podrobnosti o funkcích jsou uvedené níže.

Tyto změny neovlivní podporu verze modulu, který je součástí prostředí PowerShell a jsou kompatibilní s prostředím PowerShell 3.0 a 4.0, 5.

## <a name="identifying-a-module-version-as-a-prerelease"></a>Určení verze modulu jako zkušební verze

Podpora Správce balíčků PowerShellGet pro předběžné verze vyžaduje použití dvou polí v manifestu modulu:

- ModuleVersion součástí manifestu modulu musí být ve verzi 3 části Pokud Předběžná verze je používáno a musí být v souladu s existující verzí Powershellu. Formát verze by A.B.C, kde jsou A, B a C všech celých čísel.
- Předběžné verze řetězce je určená v manifestu modulu, v části PSData PrivateData.

Podrobné požadavky na předběžnou verzi řetězci jsou uvedené níže.

Vzorový oddíl manifestu modulu, který definuje modul jako zkušební verze by vypadat nějak takto:

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

- Předběžné verze řetězce jde zadat jenom při ModuleVersion se 3 segmenty Major.Minor.Build. Ten je v souladu s SemVer v1.0.0.
- Pomlčka je oddělovač mezi předprodejní řetězec a číslo sestavení. Pomlčka může být součástí předběžné verze řetězec jako první znak, pouze.
- Předběžné verze řetězec může obsahovat jenom alfanumerické znaky ASCII [0-9A-Za - z-]. Je nejvhodnější začít zkušební řetězce alfanumerického znaku, jak ji bude snazší zjistit, toto je předběžná verze při kontrole seznamu položek.
- V tuto chvíli jsou podporovány pouze SemVer v1.0.0 předběžné verze řetězce. Předběžné verze řetězce **nesmí** obsahovat buď období nebo + [. +], které jsou povoleny v SemVer 2.0.
- Příklady podporovaných předběžné verze řetězce:-alfa, - α1,-BETA, - update20171020

### <a name="prerelease-versioning-impact-on-sort-order-and-installation-folders"></a>Předběžné verze správy verzí dopad na složky instalace a pořadí řazení

Pořadí řazení se změní při používání předběžné verze, což je důležité při publikování do Galerie prostředí PowerShell, a při instalaci modulů pomocí příkazů PowerShellGet. Pokud se předběžné verze řetězce je zadaný pro moduly, pořadí řazení podle část řetězce po spojovník. Ano 2.5.0-alpha verze je menší než 2.5.0-beta, což je míň než 2.5.0-gamma. Pokud dva moduly mají stejné verze modulu a pouze jeden má řetězec předběžné verze, modul bez předběžné verze řetězce je považován za verze připravené pro produkční prostředí a budou seřazeny jako větší než předběžné verze (která zahrnuje zkušební verze řetězec). Jako příklad, když porovnání uvolní 2.5.0 a 2.5.0-beta, 2.5.0 verzi se budou považovat za větší z nich.

Při publikování do Galerie prostředí PowerShell, ve výchozím nastavení verze modulu zveřejněná musí mít s vyšší verzí, než všechny dříve publikované verzi, která je v galerii prostředí PowerShell.

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a>Hledání a získávání předběžnou verzi položky pomocí příkazů PowerShellGet

Práce s předběžnou verzi položek pomocí modulu – najděte – modulu PowerShellGet, Install-Module, aktualizace, a příkazy Save-Module vyžaduje přidání příznaku - AllowPrerelease. Pokud - AllowPrerelease není zadána, předběžné verze položky budou zahrnuty v případě, že jsou k dispozici. Pokud se nezadá příznak - AllowPrerelease, nezobrazí se předběžné verze položky.

Jedinou výjimkou tohoto v příkazech modulu PowerShellGet jsou Get-InstalledModule a někdy se odinstalace modulu.

- Get-InstalledModule vždy automaticky zobrazí informace o předběžnou verzi v řetězci verze pro moduly.
- Odinstalujte modul bude ve výchozím nastavení odinstalace nejnovější verzi modulu, pokud __žádná verze__ je zadán. Aby nedošlo ke změně chování. Nicméně pokud předprodejní verze určena pomocí - RequiredVersion, - AllowPrerelease se bude vyžadovat.

## <a name="examples"></a>Příklady

Předpokládejme, že má Galerie prostředí PowerShell, verze modulu TestPackage 1.8.0 a 1.9.0-alpha. Pokud `-AllowPrerelease` není zadán, bude vrácena pouze verze 1.8.0.

```powershell
find-module TestPackage
```

```output
Version        Name           Repository  Description
-------        ----           ----------  -----------
1.8.0          TestPackage    PSGallery   Package used to validate changes to the PowerShe...
```

```powershell
find-module TestPackage -AllowPrerelease
```

```output
Version        Name           Repository  Description
-------        ----           ----------  -----------
1.9.0-alpha    TestPackage    PSGallery   Package used to validate changes to the PowerShe...
```

Chcete-li nainstalovat zkušební verze, vždy zadejte - AllowPrerelease. Určení předprodejní verze řetězce není dostatečná.

```powershell
Install-module TestPackage -RequiredVersion 1.9.0-alpha
```

```output
PackageManagement\Find-Package : No match was found for the specified search criteria and module name 'TestPackage'.
Try Get-PSRepository to see all available registered module repositories.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.6.0\PSModule.psm1:1455 char:3
+         PackageManagement\Find-Package @PSBoundParameters | Microsoft ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...ets.FindPackage:FindPackage) [Find-Package], Exception
    + FullyQualifiedErrorId : NoMatchFoundForCriteria,Microsoft.PowerShell.PackageManagement.Cmdlets.FindPackage
```

Předchozí příkaz se nezdařil, protože nebyl zadán - AllowPrerelease. Přidání `-AllowPrerelease` bude mít za následek úspěšné.

```powershell
Install-module TestPackage -RequiredVersion 1.9.0-alpha -AllowPrerelease
Get-InstalledModule TestPackage
```

```output
Version         Name          Repository  Description
-------         ----          ----------  -----------
1.9.0-alpha     TestPackage   PSGallery   Package used to validate changes to the PowerShe...
```

Vedle sebe instalace verzí modulu, které se liší pouze z důvodu předběžné verze zadané není podporována. Při instalaci modulu pomocí Správce balíčků PowerShellGet, jsou různé verze stejného modulu nainstalovaného side-by-side tak, že vytvoříte pomocí ModuleVersion název složky. Verze modulu bez předprodejní řetězec se používá pro název složky. Pokud uživatel nainstaluje verzi 2.5.0-alpha MyModule, nainstaluje se na `MyModule\2.5.0` složky. Pokud uživatel pak nainstaluje 2.5.0-beta, bude verze 2.5.0-beta **přepsat** obsah složky `MyModule\2.5.0`. Jednou z výhod tohoto přístupu je, že není nutné provést odinstalaci předběžné verze po instalaci verze připravené pro produkční prostředí. Následující příklad ukazuje, co můžete očekávat:

``` powershell
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name           Repository  Description
-------         ----           ----------  -----------
1.9.0-alpha     TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.8.0           TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage    PSGallery   Package used to validate changes to the PowerShe...

C:\windows\system32> find-module TestPackage -AllowPrerelease

Version        Name            Repository  Description
-------        ----            ----------  -----------
1.9.0-beta     TestPackage     PSGallery   Package used to validate changes to the PowerShe...

C:\windows\system32> Update-Module TestPackage -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name           Repository  Description
-------         ----           ----------  -----------
1.9.0-beta      TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.8.0           TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage    PSGallery   Package used to validate changes to the PowerShe...

```

Odinstalujte modul odebere nejnovější verzi modulu, pokud není zadán - RequiredVersion.
Pokud je zadán - RequiredVersion a je zkušební verze, - AllowPrerelease musí přidat k příkazu.

``` powershell
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name           Repository  Description
-------         ----           ----------  -----------
2.0.0-alpha1    TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.9.0-beta      TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.8.0           TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage    PSGallery   Package used to validate changes to the PowerShe...

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

Version         Name          Repository   Description
-------         ----          ----------   -----------
2.0.0-alpha1    TestPackage   PSGallery    Package used to validate changes to the PowerShe...
1.8.0           TestPackage   PSGallery    Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage   PSGallery    Package used to validate changes to the PowerShe...

C:\windows\system32> Uninstall-Module TestPackage
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name          Repository   Description
-------         ----          ----------   -----------
1.8.0           TestPackage   PSGallery    Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage   PSGallery    Package used to validate changes to the PowerShe...
```

## <a name="more-details"></a>Další podrobnosti

- [Skript předprodejní verze](script-prerelease-support.md)
- [Find-Module](/powershell/module/powershellget/find-module)
- [Install-Module](/powershell/module/powershellget/install-module)
- [Save-Module](/powershell/module/powershellget/save-module)
- [Aktualizace modulu](/powershell/module/powershellget/Update-Module)
- [Get-InstalledModule](/powershell/module/powershellget/get-installedmodule)
- [Odinstalujte modul](/powershell/module/powershellget/uninstall-module)