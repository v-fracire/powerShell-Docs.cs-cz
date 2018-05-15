---
ms.date: 10/17/2017
contributor: keithb
ms.topic: reference
keywords: Galerie prostředí powershell, rutiny, psget
title: Předprodejní verze skriptů
ms.openlocfilehash: 2c7e1cbc352f8dc39fef9cd968b2f0c1964c30b3
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="prerelease-versions-of-scripts"></a><span data-ttu-id="c43a1-103">Předprodejní verze skriptů</span><span class="sxs-lookup"><span data-stu-id="c43a1-103">Prerelease versions of scripts</span></span>

<span data-ttu-id="c43a1-104">Počínaje verzí 1.6.0, PowerShellGet a Galerie prostředí PowerShell poskytuje podporu pro označování příznaky verze větší než 1.0.0 jako zkušební verze.</span><span class="sxs-lookup"><span data-stu-id="c43a1-104">Starting with version 1.6.0, PowerShellGet and the PowerShell Gallery provide support for tagging versions greater than 1.0.0 as a prerelease.</span></span> <span data-ttu-id="c43a1-105">Před touto funkcí předprodejní položky byly omezeny na situaci, kdy verze počínaje 0.</span><span class="sxs-lookup"><span data-stu-id="c43a1-105">Prior to this feature, prerelease items were limited to having a version beginning with 0.</span></span> <span data-ttu-id="c43a1-106">Cílem těchto funkcí je poskytují větší podporu pro [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) konvence Správa verzí, aniž by vás zpětnou kompatibilitu s verzemi 3 a výše uvedené nebo existující verze prostředí PowerShell služby PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="c43a1-106">The goal of these features is to provide greater support for [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning convention without breaking backwards compatibility with PowerShell versions 3 and above, or existing versions of PowerShellGet.</span></span> <span data-ttu-id="c43a1-107">Toto téma se zaměřuje na funkce specifické pro skript.</span><span class="sxs-lookup"><span data-stu-id="c43a1-107">This topic focuses on the script-specific features.</span></span> <span data-ttu-id="c43a1-108">Ekvivalentní funkce pro moduly jsou v [předběžné verze modulu verze](module-prerelease-support.md) tématu.</span><span class="sxs-lookup"><span data-stu-id="c43a1-108">The equivalent features for modules are in the [Prerelease Module Versions](module-prerelease-support.md) topic.</span></span> <span data-ttu-id="c43a1-109">Používání těchto funkcí, vydavatelů můžete identifikovat skript jako verze 2.5.0-alpha a novější verze na produkční prostředí verzi 2.5.0, která nahrazuje předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="c43a1-109">Using these features, publishers can identify a script as version 2.5.0-alpha, and later release a production-ready version 2.5.0 that supersedes the prerelease version.</span></span>

<span data-ttu-id="c43a1-110">Na vysoké úrovni funkce předběžné verze skriptu patří:</span><span class="sxs-lookup"><span data-stu-id="c43a1-110">At a high level, the prerelease script features include:</span></span>

- <span data-ttu-id="c43a1-111">Přidání přípony PrereleaseString na řetězec verze ve skriptu manifest.</span><span class="sxs-lookup"><span data-stu-id="c43a1-111">Adding a PrereleaseString suffix to the version string in the script manifest.</span></span> <span data-ttu-id="c43a1-112">Pokud skripty je publikovaná v galerii prostředí PowerShell, tato data jsou extrahovány z manifestu a použít k identifikaci předprodejní položky.</span><span class="sxs-lookup"><span data-stu-id="c43a1-112">When the scripts is published to the PowerShell Gallery, this data is extracted from the manifest, and used to identify prerelease items.</span></span>
- <span data-ttu-id="c43a1-113">Získávání předprodejní položky vyžaduje přidání příznak - AllowPrerelease PowerShellGet příkazy skriptu najít instalační skript, skript aktualizace a uložit skript.</span><span class="sxs-lookup"><span data-stu-id="c43a1-113">Acquiring prerelease items requires adding -AllowPrerelease flag to the PowerShellGet commands Find-Script, Install-Script, Update-Script, and Save-Script.</span></span> <span data-ttu-id="c43a1-114">Pokud není zadán příznak, nebude se zobrazovat předprodejní položky.</span><span class="sxs-lookup"><span data-stu-id="c43a1-114">If the flag is not specified, prerelease items will not be shown.</span></span>
- <span data-ttu-id="c43a1-115">Verze skriptu zobrazí najít-skript, Get-InstalledScript a v galerii prostředí PowerShell se zobrazí PrereleaseString, stejně jako 2.5.0-alpha.</span><span class="sxs-lookup"><span data-stu-id="c43a1-115">Script versions displayed by Find-Script, Get-InstalledScript, and in the PowerShell Gallery will be displayed with the PrereleaseString, as in 2.5.0-alpha.</span></span>

<span data-ttu-id="c43a1-116">Podrobnosti pro funkce, které jsou popsány níže.</span><span class="sxs-lookup"><span data-stu-id="c43a1-116">Details for the features are included below.</span></span>

## <a name="identifying-a-script-version-as-a-prerelease"></a><span data-ttu-id="c43a1-117">Identifikace verze skriptu jako zkušební verze</span><span class="sxs-lookup"><span data-stu-id="c43a1-117">Identifying a script version as a prerelease</span></span>

<span data-ttu-id="c43a1-118">Podpora PowerShellGet pro předběžné verze je snazší pro skripty než moduly.</span><span class="sxs-lookup"><span data-stu-id="c43a1-118">PowerShellGet support for prerelease versions is easier for scripts than modules.</span></span> <span data-ttu-id="c43a1-119">Správa verzí skriptu je podporována pouze PowerShellGet, proto nejsou žádné problémy s kompatibilitou způsobené přidání předprodejní řetězec.</span><span class="sxs-lookup"><span data-stu-id="c43a1-119">Script versioning is only supported by PowerShellGet, so there are no compatibility issues caused by adding the prerelease string.</span></span> <span data-ttu-id="c43a1-120">K identifikaci skript v galerii prostředí PowerShell jako zkušební verze, přidejte příponu předprodejní na řetězec správně naformátován verzi v metadatech skriptu.</span><span class="sxs-lookup"><span data-stu-id="c43a1-120">To identify a script in the PowerShell Gallery as a prerelease, add a prerelease suffix to a properly-formatted version string in the script metadata.</span></span>

<span data-ttu-id="c43a1-121">Na příkladu část skriptu manifest s předprodejní verze by vypadat následovně:</span><span class="sxs-lookup"><span data-stu-id="c43a1-121">An example section of a script manifest with a prerelease version would look like the following:</span></span>

```powershell
<#PSScriptInfo

.VERSION 3.2.1-alpha12

.GUID

...

#>

```

<span data-ttu-id="c43a1-122">Pokud chcete používat příponu předprodejní, řetězec verze musí splňovat následující požadavky:</span><span class="sxs-lookup"><span data-stu-id="c43a1-122">To use a prerelease suffix, the version string must meet the following requirements:</span></span>

- <span data-ttu-id="c43a1-123">Předběžné verze příponu lze zadat pouze pokud je verze 3 segmenty pro Major.Minor.Build.</span><span class="sxs-lookup"><span data-stu-id="c43a1-123">A prerelease suffix may only be specified when the Version is 3 segments for Major.Minor.Build.</span></span>
  <span data-ttu-id="c43a1-124">To zarovnaná s SemVer v1.0.0</span><span class="sxs-lookup"><span data-stu-id="c43a1-124">This aligns with SemVer v1.0.0</span></span>
- <span data-ttu-id="c43a1-125">Předběžné verze přípona je řetězec, který začíná pomlčka a může obsahovat alfanumerické znaky ASCII [0-9A-Za - z –]</span><span class="sxs-lookup"><span data-stu-id="c43a1-125">The prerelease suffix is a string which begins with a hyphen, and may contain ASCII alphanumerics [0-9A-Za-z-]</span></span>
- <span data-ttu-id="c43a1-126">Pouze SemVer v1.0.0 předprodejní řetězce jsou podporovány v tuto chvíli tak předprodejní přípona __musí není__ obsahovat buď období nebo + [. +], které jsou povoleny v SemVer 2.0</span><span class="sxs-lookup"><span data-stu-id="c43a1-126">Only SemVer v1.0.0 prerelease strings are supported at this time, so the prerelease suffix __must not__ contain either period or + [.+], which are allowed in SemVer 2.0</span></span>
- <span data-ttu-id="c43a1-127">Příklady podporovaných řetězců PrereleaseString:-alpha, - α1,-BETA, - update20171020</span><span class="sxs-lookup"><span data-stu-id="c43a1-127">Examples of supported PrereleaseString strings are: -alpha, -alpha1, -BETA, -update20171020</span></span>

<span data-ttu-id="c43a1-128">__Předprodejní verze dopad na složky instalace a pořadí řazení__</span><span class="sxs-lookup"><span data-stu-id="c43a1-128">__Prerelease versioning impact on sort order and installation folders__</span></span>

<span data-ttu-id="c43a1-129">Pořadí řazení se změní při použití předprodejní verze, což je důležité při publikování do Galerie prostředí PowerShell, a při instalaci pomocí příkazů PowerShellGet skripty.</span><span class="sxs-lookup"><span data-stu-id="c43a1-129">Sort order changes when using a prerelease version, which is important when publishing to the PowerShell Gallery, and when installing scripts using PowerShellGet commands.</span></span> <span data-ttu-id="c43a1-130">Pokud dvě verze číslo verze skriptů existují, pořadí řazení podle části řetězce následující spojovník.</span><span class="sxs-lookup"><span data-stu-id="c43a1-130">If two scripts versions with the version number exist, the sort order is based on the string portion following the hyphen.</span></span> <span data-ttu-id="c43a1-131">Ano 2.5.0-alpha verze je menší než 2.5.0-beta, která je menší než 2.5.0-gamma.</span><span class="sxs-lookup"><span data-stu-id="c43a1-131">So, version 2.5.0-alpha is less than 2.5.0-beta, which is less than 2.5.0-gamma.</span></span> <span data-ttu-id="c43a1-132">Pokud dva skripty mít stejné číslo verze a jenom jedna má PrereleaseString, skript __bez__ předprodejní příponu se předpokládá, že jako verze na produkční prostředí a seřadí jako vyšší verzi než zkušební verze.</span><span class="sxs-lookup"><span data-stu-id="c43a1-132">If two scripts have the same version number, and only one has a PrereleaseString, the script __without__ the prerelease suffix is assumed to be the production-ready version and will be sorted as a greater version than the prerelease version.</span></span> <span data-ttu-id="c43a1-133">Jako příklad, při porovnání uvolní 2.5.0 a 2.5.0-beta, 2.5.0 verze bude považovat za delší než dva.</span><span class="sxs-lookup"><span data-stu-id="c43a1-133">As an example, when comparing releases 2.5.0 and 2.5.0-beta, the 2.5.0 version will be considered the greater of the two.</span></span>

<span data-ttu-id="c43a1-134">Při publikování do Galerie prostředí PowerShell, ve výchozím nastavení verze skriptu publikovanému musí mít vyšší verzi než všechny dříve publikované verze, která je v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c43a1-134">When publishing to the PowerShell Gallery, by default the version of the script being published must have a greater version than any previously-published version that is in the PowerShell Gallery.</span></span> <span data-ttu-id="c43a1-135">Vydavatelem může aktualizovat verzi 2.5.0-alpha 2.5.0-beta nebo s 2.5.0 (s příponou žádné předprodejní).</span><span class="sxs-lookup"><span data-stu-id="c43a1-135">A publisher may update version 2.5.0-alpha with 2.5.0-beta, or with 2.5.0 (with no prerelease suffix).</span></span>

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a><span data-ttu-id="c43a1-136">Hledání a získávání předprodejní položek pomocí PowerShellGet příkazy</span><span class="sxs-lookup"><span data-stu-id="c43a1-136">Finding and acquiring prerelease items using PowerShellGet commands</span></span>

<span data-ttu-id="c43a1-137">Plánování práce s předprodejní položek pomocí skript-PowerShellGet najít skriptu, instalační skript, aktualizace, a příkazy skriptu uložit vyžaduje přidání příznak - AllowPrerelease.</span><span class="sxs-lookup"><span data-stu-id="c43a1-137">Dealing with prerelease items using PowerShellGet Find-Script, Install-Script, Update-Script, and Save-Script commands requires adding the -AllowPrerelease flag.</span></span> <span data-ttu-id="c43a1-138">Pokud je zadán - AllowPrerelease, předprodejní položky budou zahrnuty, pokud jsou přítomna.</span><span class="sxs-lookup"><span data-stu-id="c43a1-138">If -AllowPrerelease is specified, prerelease items will be included if they are present.</span></span> <span data-ttu-id="c43a1-139">Pokud není zadán příznak - AllowPrerelease, nebude se zobrazovat předprodejní položky.</span><span class="sxs-lookup"><span data-stu-id="c43a1-139">If -AllowPrerelease flag is not specified, prerelease items will not be shown.</span></span>

<span data-ttu-id="c43a1-140">To v příkazy skriptu PowerShellGet jedinou výjimkou jsou Get-InstalledScript a někdy s odinstalační skript.</span><span class="sxs-lookup"><span data-stu-id="c43a1-140">The only exceptions to this in the PowerShellGet script commands are Get-InstalledScript, and some cases with Uninstall-Script.</span></span>

- <span data-ttu-id="c43a1-141">Get-InstalledScript vždy se automaticky zobrazí předběžné informace v řetězec verze pokud je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="c43a1-141">Get-InstalledScript always will automatically show the prerelease information in the version string if it is present.</span></span>
- <span data-ttu-id="c43a1-142">Odinstalujte skript bude ve výchozím nastavení nejnovější verzi odinstalujte skriptu, pokud __žádná verze__ je zadán.</span><span class="sxs-lookup"><span data-stu-id="c43a1-142">Uninstall-Script will by default uninstall the most recent version of a script, if __no version__ is specified.</span></span> <span data-ttu-id="c43a1-143">Daná chování se nezměnilo.</span><span class="sxs-lookup"><span data-stu-id="c43a1-143">That behavior has not changed.</span></span> <span data-ttu-id="c43a1-144">Ale pokud předprodejní verze je zadán pomocí - RequiredVersion, - AllowPrerelease se bude vyžadovat.</span><span class="sxs-lookup"><span data-stu-id="c43a1-144">However, if a prerelease version is specified using -RequiredVersion, -AllowPrerelease will be required.</span></span>

## <a name="examples"></a><span data-ttu-id="c43a1-145">Příklady</span><span class="sxs-lookup"><span data-stu-id="c43a1-145">Examples</span></span>

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

<span data-ttu-id="c43a1-146">Odinstalujte skriptu odebere aktuální verze skriptu, pokud není zadáno - RequiredVersion.</span><span class="sxs-lookup"><span data-stu-id="c43a1-146">Uninstall-Script will remove the current version of a script when -RequiredVersion is not supplied.</span></span>
<span data-ttu-id="c43a1-147">Pokud - RequiredVersion byl zadán a je předběžné verze, - AllowPrerelease je nutné přidat do příkazu.</span><span class="sxs-lookup"><span data-stu-id="c43a1-147">If -RequiredVersion is specified, and is a prerelease, -AllowPrerelease must be added to the command.</span></span>

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

## <a name="more-details"></a><span data-ttu-id="c43a1-148">Další informace</span><span class="sxs-lookup"><span data-stu-id="c43a1-148">More details</span></span>

- [<span data-ttu-id="c43a1-149">Modul předprodejní verze</span><span class="sxs-lookup"><span data-stu-id="c43a1-149">Prerelease Module Versions</span></span>](module-prerelease-support.md)
- [<span data-ttu-id="c43a1-150">Najít skriptu</span><span class="sxs-lookup"><span data-stu-id="c43a1-150">Find-script</span></span>](/powershell/module/powershellget/find-script)
- [<span data-ttu-id="c43a1-151">Instalační skript</span><span class="sxs-lookup"><span data-stu-id="c43a1-151">Install-script</span></span>](/powershell/module/powershellget/install-script)
- [<span data-ttu-id="c43a1-152">Uložení skriptu</span><span class="sxs-lookup"><span data-stu-id="c43a1-152">Save-script</span></span>](/powershell/module/powershellget/save-script)
- [<span data-ttu-id="c43a1-153">Skript aktualizace</span><span class="sxs-lookup"><span data-stu-id="c43a1-153">Update-script</span></span>](/powershell/module/powershellget/update-script)
- [<span data-ttu-id="c43a1-154">Get-Installedscript</span><span class="sxs-lookup"><span data-stu-id="c43a1-154">Get-Installedscript</span></span>](/powershell/module/powershellget/get-installedscript)
- [<span data-ttu-id="c43a1-155">Odinstalujte skriptu</span><span class="sxs-lookup"><span data-stu-id="c43a1-155">UnInstall-script</span></span>](/powershell/module/powershellget/uninstall-script)