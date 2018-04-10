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
# <a name="prerelease-module-versions"></a><span data-ttu-id="d435d-103">Modul předprodejní verze</span><span class="sxs-lookup"><span data-stu-id="d435d-103">Prerelease Module Versions</span></span>
<span data-ttu-id="d435d-104">Počínaje verzí 1.6.0, PowerShellGet a Galerie prostředí PowerShell poskytuje podporu pro označování příznaky verze větší než 1.0.0 jako zkušební verze.</span><span class="sxs-lookup"><span data-stu-id="d435d-104">Starting with version 1.6.0, PowerShellGet and the PowerShell Gallery provide support for tagging versions greater than 1.0.0 as a prerelease.</span></span> <span data-ttu-id="d435d-105">Před touto funkcí předprodejní položky byly omezeny na situaci, kdy verze počínaje 0.</span><span class="sxs-lookup"><span data-stu-id="d435d-105">Prior to this feature, prerelease items were limited to having a version beginning with 0.</span></span> <span data-ttu-id="d435d-106">Cílem těchto funkcí je poskytují větší podporu pro [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) konvence Správa verzí, aniž by vás zpětnou kompatibilitu s verzemi 3 a výše uvedené nebo existující verze prostředí PowerShell služby PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="d435d-106">The goal of these features is to provide greater support for [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning convention without breaking backwards compatibility with PowerShell versions 3 and above, or existing versions of PowerShellGet.</span></span> <span data-ttu-id="d435d-107">Toto téma se zaměřuje na funkce specifické pro modul.</span><span class="sxs-lookup"><span data-stu-id="d435d-107">This topic focuses on the module-specific features.</span></span> <span data-ttu-id="d435d-108">Ekvivalentní funkce skriptů jsou v [vydanou verzí skripty](../script/PrereleaseScript.md) tématu.</span><span class="sxs-lookup"><span data-stu-id="d435d-108">The equivalent features for scripts are in the [Prerelease Versions of Scripts](../script/PrereleaseScript.md) topic.</span></span> <span data-ttu-id="d435d-109">Používání těchto funkcí, vydavatelů můžete identifikovat modulu nebo skriptu jako verze 2.5.0-alpha a novější verze na produkční prostředí verzi 2.5.0, která nahrazuje předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="d435d-109">Using these features, publishers can identify a module or script as version 2.5.0-alpha, and later release a production-ready version 2.5.0 that supersedes the prerelease version.</span></span>

<span data-ttu-id="d435d-110">Na vysoké úrovni funkce předběžné verze modulu patří:</span><span class="sxs-lookup"><span data-stu-id="d435d-110">At a high level, the prerelease module features include:</span></span>

* <span data-ttu-id="d435d-111">Přidání předprodejní řetězec do části PSData manifestu modulu identifikuje modul jako předprodejní verze.</span><span class="sxs-lookup"><span data-stu-id="d435d-111">Adding a Prerelease string to the PSData section of the module manifest identifies the module as a prerelease version.</span></span>
<span data-ttu-id="d435d-112">Pokud modul je publikovaná v galerii prostředí PowerShell, tato data jsou extrahovány z manifestu a použít k identifikaci předprodejní položky.</span><span class="sxs-lookup"><span data-stu-id="d435d-112">When the module is published to the PowerShell Gallery, this data is extracted from the manifest, and used to identify prerelease items.</span></span>
* <span data-ttu-id="d435d-113">Získávání předprodejní položky vyžaduje přidání příznak - AllowPrerelease PowerShellGet příkazy najít-Module instalace modulu, aktualizace modulu a uložit modulu.</span><span class="sxs-lookup"><span data-stu-id="d435d-113">Acquiring prerelease items requires adding -AllowPrerelease flag to the PowerShellGet commands Find-Module, Install-Module, Update-Module, and Save-Module.</span></span>
<span data-ttu-id="d435d-114">Pokud není zadán příznak, nebude se zobrazovat předprodejní položky.</span><span class="sxs-lookup"><span data-stu-id="d435d-114">If the flag is not specified, prerelease items will not be shown.</span></span>
* <span data-ttu-id="d435d-115">Verze modulu zobrazovat najít-modulu, Get-InstalledModule a v galerii prostředí PowerShell se zobrazí jako jeden řetězec předprodejní řetězcem, který připojí jako 2.5.0-alpha.</span><span class="sxs-lookup"><span data-stu-id="d435d-115">Module versions displayed by Find-Module, Get-InstalledModule, and in the PowerShell Gallery will be displayed as a single string with the Prerelease string appended, as in 2.5.0-alpha.</span></span>

<span data-ttu-id="d435d-116">Podrobnosti pro funkce, které jsou popsány níže.</span><span class="sxs-lookup"><span data-stu-id="d435d-116">Details for the features are included below.</span></span>

<span data-ttu-id="d435d-117">Tyto změny neovlivňují podpora verze modulu, který je součástí prostředí PowerShell a jsou kompatibilní s prostředím PowerShell 3.0, 4.0 a 5.</span><span class="sxs-lookup"><span data-stu-id="d435d-117">These changes do not affect the module version support that is built into PowerShell, and are compatible with PowerShell 3.0, 4.0, and 5.</span></span>

## <a name="identifying-a-module-version-as-a-prerelease"></a><span data-ttu-id="d435d-118">Identifikace verze modulu jako zkušební verze</span><span class="sxs-lookup"><span data-stu-id="d435d-118">Identifying a module version as a prerelease</span></span>

<span data-ttu-id="d435d-119">Podpora PowerShellGet pro předběžné verze vyžaduje použití dvě pole v manifestu modulu:</span><span class="sxs-lookup"><span data-stu-id="d435d-119">PowerShellGet support for prerelease versions requires the use of two fields within the Module Manifest:</span></span>

* <span data-ttu-id="d435d-120">Verze modulu zahrnuté v manifestu modulu musí být verze 3 část, pokud předprodejní verze se používá a musí být v souladu s existující verze prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d435d-120">The ModuleVersion included in the module manifest must be a 3-part version if a prerelease version is used, and must comply with existing PowerShell versioning.</span></span> <span data-ttu-id="d435d-121">Verze formátu by A.B.C, kde A, B a C jsou všechny celá čísla.</span><span class="sxs-lookup"><span data-stu-id="d435d-121">The version format would be A.B.C, where A, B, and C are all integers.</span></span>
* <span data-ttu-id="d435d-122">Předběžné verze řetězec je zadáno v manifestu modulu, v části PSData PrivateData.</span><span class="sxs-lookup"><span data-stu-id="d435d-122">The Prerelease string is specified in the module manifest, in the PSData section of PrivateData.</span></span>
<span data-ttu-id="d435d-123">Podrobné požadavky na předprodejní řetězce jsou níže.</span><span class="sxs-lookup"><span data-stu-id="d435d-123">Detailed requirements on the Prerelease string are below.</span></span>

<span data-ttu-id="d435d-124">Příklad části modul manifestu, který definuje modul jako zkušební verze by vypadat třeba takto:</span><span class="sxs-lookup"><span data-stu-id="d435d-124">An example section of a module manifest that defines a module as a prerelease would look like the following:</span></span>
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

<span data-ttu-id="d435d-125">Podrobné požadavky pro předběžné verze řetězce jsou:</span><span class="sxs-lookup"><span data-stu-id="d435d-125">The detailed requirements for Prerelease string are:</span></span>

* <span data-ttu-id="d435d-126">Předběžné verze řetězec lze zadat pouze pokud verze modulu 3 segmenty pro Major.Minor.Build.</span><span class="sxs-lookup"><span data-stu-id="d435d-126">Prerelease string may only be specified when the ModuleVersion is 3 segments for Major.Minor.Build.</span></span> <span data-ttu-id="d435d-127">To zarovnaná s SemVer v1.0.0.</span><span class="sxs-lookup"><span data-stu-id="d435d-127">This aligns with SemVer v1.0.0.</span></span>
* <span data-ttu-id="d435d-128">Pomlčka je odděleny číslo sestavení a předběžné verze řetězce.</span><span class="sxs-lookup"><span data-stu-id="d435d-128">A hyphen is the delimiter between the Build number and the Prerelease string.</span></span> <span data-ttu-id="d435d-129">Pomlčka může být součástí předběžné verze řetězec jako první znak, pouze.</span><span class="sxs-lookup"><span data-stu-id="d435d-129">A hyphen may be included in the Prerelease string as the first character, only.</span></span>
* <span data-ttu-id="d435d-130">Předběžné verze řetězce mohou obsahovat pouze alfanumerické znaky ASCII [0-9A-Za - z –].</span><span class="sxs-lookup"><span data-stu-id="d435d-130">The Prerelease string may contain only ASCII alphanumerics [0-9A-Za-z-].</span></span> <span data-ttu-id="d435d-131">Je osvědčeným postupem zahájit zkušební řetězce s alfanumerický znak, jako je jednodušší zjistit, to je předprodejní verze při kontrole seznam položek.</span><span class="sxs-lookup"><span data-stu-id="d435d-131">It is a best practice to begin the Prerelease string with an alpha character, as it will be easier to identify that this is a prerelease version when scanning a list of items.</span></span>
* <span data-ttu-id="d435d-132">V tuto chvíli jsou podporovány pouze SemVer v1.0.0 předprodejní řetězce.</span><span class="sxs-lookup"><span data-stu-id="d435d-132">Only SemVer v1.0.0 prerelease strings are supported at this time.</span></span> <span data-ttu-id="d435d-133">Předběžné verze řetězec __musí není__ obsahovat buď období nebo + [. +], které jsou povoleny v SemVer 2.0.</span><span class="sxs-lookup"><span data-stu-id="d435d-133">Prerelease string __must not__ contain either period or + [.+], which are allowed in SemVer 2.0.</span></span>
* <span data-ttu-id="d435d-134">Příklady podporovaných předprodejní řetězec:-alpha, - α1,-BETA, - update20171020</span><span class="sxs-lookup"><span data-stu-id="d435d-134">Examples of supported Prerelease string are: -alpha, -alpha1, -BETA, -update20171020</span></span>

<span data-ttu-id="d435d-135">__Předprodejní verze dopad na složky instalace a pořadí řazení__</span><span class="sxs-lookup"><span data-stu-id="d435d-135">__Prerelease versioning impact on sort order and installation folders__</span></span>

<span data-ttu-id="d435d-136">Pořadí řazení se změní při použití předprodejní verze, což je důležité při publikování do Galerie prostředí PowerShell, a při instalaci modulů pomocí PowerShellGet příkazy.</span><span class="sxs-lookup"><span data-stu-id="d435d-136">Sort order changes when using a prerelease version, which is important when publishing to the PowerShell Gallery, and when installing modules using PowerShellGet commands.</span></span>
<span data-ttu-id="d435d-137">Pokud předprodejní řetězec je zadán pro dva moduly, pořadí řazení podle části řetězce následující spojovník.</span><span class="sxs-lookup"><span data-stu-id="d435d-137">If the Prerelease string is specified for two modules, the sort order is based on the string portion following the hyphen.</span></span> <span data-ttu-id="d435d-138">Ano 2.5.0-alpha verze je menší než 2.5.0-beta, která je menší než 2.5.0-gamma.</span><span class="sxs-lookup"><span data-stu-id="d435d-138">So, version 2.5.0-alpha is less than 2.5.0-beta, which is less than 2.5.0-gamma.</span></span>
<span data-ttu-id="d435d-139">Pokud dva moduly mají stejné verze modulu a jenom jedna má předprodejní řetězec, se předpokládá, že jako verze na produkční prostředí a seřadí jako vyšší verzi než předprodejní verze (která zahrnuje zkušební modul bez předprodejní řetězec řetězec).</span><span class="sxs-lookup"><span data-stu-id="d435d-139">If two modules have the same ModuleVersion, and only one has a Prerelease string, the module without the Prerelease string is assumed to be the production-ready version and will be sorted as a greater version than the prerelease version (which includes the Prerelease string).</span></span>
<span data-ttu-id="d435d-140">Jako příklad, při porovnání uvolní 2.5.0 a 2.5.0-beta, 2.5.0 verze bude považovat za delší než dva.</span><span class="sxs-lookup"><span data-stu-id="d435d-140">As an example, when comparing releases 2.5.0 and 2.5.0-beta, the 2.5.0 version will be considered the greater of the two.</span></span>

<span data-ttu-id="d435d-141">Při publikování do Galerie prostředí PowerShell, ve výchozím nastavení verzi modulu publikovanému musí mít vyšší verzi než všechny dříve publikované verze, která je v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d435d-141">When publishing to the PowerShell Gallery, by default the version of the module being published must have a greater version than any previously-published version that is in the PowerShell Gallery.</span></span>

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a><span data-ttu-id="d435d-142">Hledání a získávání předprodejní položek pomocí PowerShellGet příkazy</span><span class="sxs-lookup"><span data-stu-id="d435d-142">Finding and acquiring prerelease items using PowerShellGet commands</span></span>

<span data-ttu-id="d435d-143">Plánování práce s předprodejní položek pomocí modulu-najít PowerShellGet-Module, instalace modulu, aktualizace, a příkazy Uložit-Module vyžaduje přidání příznak - AllowPrerelease.</span><span class="sxs-lookup"><span data-stu-id="d435d-143">Dealing with prerelease items using PowerShellGet Find-Module, Install-Module, Update-Module, and Save-Module commands requires adding the -AllowPrerelease flag.</span></span>
<span data-ttu-id="d435d-144">Pokud je zadán - AllowPrerelease, předprodejní položky budou zahrnuty, pokud jsou přítomna.</span><span class="sxs-lookup"><span data-stu-id="d435d-144">If -AllowPrerelease is specified, prerelease items will be included if they are present.</span></span>
<span data-ttu-id="d435d-145">Pokud není zadán příznak - AllowPrerelease, nebude se zobrazovat předprodejní položky.</span><span class="sxs-lookup"><span data-stu-id="d435d-145">If -AllowPrerelease flag is not specified, prerelease items will not be shown.</span></span>

<span data-ttu-id="d435d-146">To v příkazech modulu PowerShellGet jedinou výjimkou jsou Get-InstalledModule a někdy modulem odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="d435d-146">The only exceptions to this in the PowerShellGet module commands are Get-InstalledModule, and some cases with Uninstall-Module.</span></span>

* <span data-ttu-id="d435d-147">Get-InstalledModule vždy se automaticky zobrazí předběžné informace v řetězec verze pro moduly.</span><span class="sxs-lookup"><span data-stu-id="d435d-147">Get-InstalledModule always will automatically show the prerelease information in the version string for modules.</span></span>
* <span data-ttu-id="d435d-148">Odinstalujte modul bude ve výchozím nastavení nejnovější verzi odinstalujte modul, pokud __žádná verze__ je zadán.</span><span class="sxs-lookup"><span data-stu-id="d435d-148">Uninstall-Module will by default uninstall the most recent version of a module, if __no version__ is specified.</span></span> <span data-ttu-id="d435d-149">Daná chování se nezměnilo.</span><span class="sxs-lookup"><span data-stu-id="d435d-149">That behavior has not changed.</span></span> <span data-ttu-id="d435d-150">Ale pokud předprodejní verze je zadán pomocí - RequiredVersion, - AllowPrerelease se bude vyžadovat.</span><span class="sxs-lookup"><span data-stu-id="d435d-150">However, if a prerelease version is specified using -RequiredVersion, -AllowPrerelease will be required.</span></span>

## <a name="examples"></a><span data-ttu-id="d435d-151">Příklady</span><span class="sxs-lookup"><span data-stu-id="d435d-151">Examples</span></span>
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

<span data-ttu-id="d435d-152">Souběžně sdílená instalace verze modulu, které se liší pouze z důvodu předběžné verze zadané není podporována.</span><span class="sxs-lookup"><span data-stu-id="d435d-152">Side-by-side installation of versions of a module that differ only due to the prerelease specified is not supported.</span></span>
<span data-ttu-id="d435d-153">Při instalaci modulu pomocí PowerShellGet, jsou různé verze stejného modulu nainstalované-souběžného vytvořením název složky pomocí verze modulu.</span><span class="sxs-lookup"><span data-stu-id="d435d-153">When installing a module using PowerShellGet, different versions of the same module are installed side-by-side by creating a folder name using the ModuleVersion.</span></span>
<span data-ttu-id="d435d-154">Verze modulu, bez předprodejní řetězec se používá v názvu složky.</span><span class="sxs-lookup"><span data-stu-id="d435d-154">The ModuleVersion, without the prerelease string, is used for the folder name.</span></span>
<span data-ttu-id="d435d-155">Pokud uživatel nainstaluje verzi 2.5.0-alpha MyModule, nainstaluje se do složky MyModule\2.5.0.</span><span class="sxs-lookup"><span data-stu-id="d435d-155">If a user installs MyModule version 2.5.0-alpha, it will be installed to the MyModule\2.5.0 folder.</span></span>
<span data-ttu-id="d435d-156">Pokud uživatel potom nainstaluje 2.5.0-beta, bude verze 2.5.0-beta __přečerpání zápisu__ obsah složky MyModule\2.5.0.</span><span class="sxs-lookup"><span data-stu-id="d435d-156">If the user then installs 2.5.0-beta, the 2.5.0-beta version will __over-write__ the contents of the folder MyModule\2.5.0.</span></span>
<span data-ttu-id="d435d-157">Jednou z výhod tohoto přístupu je, že není nutné provést odinstalaci Tuto předprodejní verzi po instalaci verze produkční prostředí.</span><span class="sxs-lookup"><span data-stu-id="d435d-157">One advantage to this approach is that there is no need to un-install the prerelease version after installing the production-ready version.</span></span>
<span data-ttu-id="d435d-158">Následující příklad ukazuje, co můžete očekávat:</span><span class="sxs-lookup"><span data-stu-id="d435d-158">The example below shows what to expect:</span></span>


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

<span data-ttu-id="d435d-159">Odinstalujte modul odeberete nejnovější verzi modulu, pokud není zadáno - RequiredVersion.</span><span class="sxs-lookup"><span data-stu-id="d435d-159">Uninstall-Module will remove the latest version of a module when -RequiredVersion is not supplied.</span></span>
<span data-ttu-id="d435d-160">Pokud - RequiredVersion byl zadán a je předběžné verze, - AllowPrerelease je nutné přidat do příkazu.</span><span class="sxs-lookup"><span data-stu-id="d435d-160">If -RequiredVersion is specified, and is a prerelease, -AllowPrerelease must be added to the command.</span></span>

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



## <a name="more-details"></a><span data-ttu-id="d435d-161">Další informace</span><span class="sxs-lookup"><span data-stu-id="d435d-161">More details</span></span>
### <a name="prerelease-script-versionsscriptprereleasescriptmd"></a>[<span data-ttu-id="d435d-162">Skript předprodejní verze</span><span class="sxs-lookup"><span data-stu-id="d435d-162">Prerelease Script Versions</span></span>](../script/PrereleaseScript.md)
### <a name="find-modulepsgetfind-modulemd"></a>[<span data-ttu-id="d435d-163">Najít – modul</span><span class="sxs-lookup"><span data-stu-id="d435d-163">Find-Module</span></span>](./psget_find-module.md)
### <a name="install-modulepsgetinstall-modulemd"></a>[<span data-ttu-id="d435d-164">Instalace modulu</span><span class="sxs-lookup"><span data-stu-id="d435d-164">Install-Module</span></span>](./psget_install-module.md)
### <a name="save-modulepsgetsave-modulemd"></a>[<span data-ttu-id="d435d-165">Save-Module</span><span class="sxs-lookup"><span data-stu-id="d435d-165">Save-Module</span></span>](./psget_save-module.md)
### <a name="update-modulepsgetupdate-modulemd"></a>[<span data-ttu-id="d435d-166">Update-Module</span><span class="sxs-lookup"><span data-stu-id="d435d-166">Update-Module</span></span>](./psget_update-module.md)
### <a name="get-installedmodulepsgetget-installedmodulemd"></a>[<span data-ttu-id="d435d-167">Get-InstalledModule</span><span class="sxs-lookup"><span data-stu-id="d435d-167">Get-InstalledModule</span></span>](./psget_get-installedmodule.md)
### <a name="uninstall-modulepsgetuninstall-modulemd"></a>[<span data-ttu-id="d435d-168">Odinstalujte modul</span><span class="sxs-lookup"><span data-stu-id="d435d-168">UnInstall-Module</span></span>](./psget_uninstall-module.md)