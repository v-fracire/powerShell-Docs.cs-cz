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
# <a name="prerelease-versions-of-scripts"></a><span data-ttu-id="2e7ce-103">Předběžné verze skriptů</span><span class="sxs-lookup"><span data-stu-id="2e7ce-103">Prerelease versions of scripts</span></span>

<span data-ttu-id="2e7ce-104">Od verze 1.6.0, Správce balíčků PowerShellGet a Galerie prostředí PowerShell poskytuje podporu pro označování verze větší než 1.0.0 jako zkušební verze.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-104">Starting with version 1.6.0, PowerShellGet and the PowerShell Gallery provide support for tagging versions greater than 1.0.0 as a prerelease.</span></span> <span data-ttu-id="2e7ce-105">Před tato funkce předběžné verze položky byly omezeny s tím, že verze počínaje 0.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-105">Prior to this feature, prerelease items were limited to having a version beginning with 0.</span></span> <span data-ttu-id="2e7ce-106">Cílem těchto funkcí je poskytují větší podporu pro [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) konvence správy verzí bez narušení zpětnou kompatibilitu s verzí Powershellu 3 a vyšší nebo stávající verze Správce balíčků PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-106">The goal of these features is to provide greater support for [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning convention without breaking backwards compatibility with PowerShell versions 3 and above, or existing versions of PowerShellGet.</span></span> <span data-ttu-id="2e7ce-107">Toto téma se zaměřuje na funkce specifické pro skript.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-107">This topic focuses on the script-specific features.</span></span> <span data-ttu-id="2e7ce-108">Ekvivalentní funkce pro moduly jsou [zkušební verze modulu](module-prerelease-support.md) tématu.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-108">The equivalent features for modules are in the [Prerelease Module Versions](module-prerelease-support.md) topic.</span></span> <span data-ttu-id="2e7ce-109">Pomocí těchto funkcí, vydavatele můžete identifikovat skript jako verze 2.5.0-alpha a novější verze produkční prostředí 2.5.0, který nahrazuje tuto předprodejní verzi.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-109">Using these features, publishers can identify a script as version 2.5.0-alpha, and later release a production-ready version 2.5.0 that supersedes the prerelease version.</span></span>

<span data-ttu-id="2e7ce-110">Na vysoké úrovni funkce předběžné verze skriptu patří:</span><span class="sxs-lookup"><span data-stu-id="2e7ce-110">At a high level, the prerelease script features include:</span></span>

- <span data-ttu-id="2e7ce-111">Přidání přípony PrereleaseString řetězec verze v manifestu skriptu.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-111">Adding a PrereleaseString suffix to the version string in the script manifest.</span></span> <span data-ttu-id="2e7ce-112">Při publikování skripty v galerii prostředí PowerShell tato data jsou extrahovány z manifestu a slouží k identifikaci předběžné verze položky.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-112">When the scripts is published to the PowerShell Gallery, this data is extracted from the manifest, and used to identify prerelease items.</span></span>
- <span data-ttu-id="2e7ce-113">Získání položky předběžné verze vyžaduje přidání příznak - AllowPrerelease do příkazů PowerShellGet Find-Script instalační skript, skript pro aktualizaci a Save-Script.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-113">Acquiring prerelease items requires adding -AllowPrerelease flag to the PowerShellGet commands Find-Script, Install-Script, Update-Script, and Save-Script.</span></span> <span data-ttu-id="2e7ce-114">Pokud se nezadá příznak, nezobrazí se předběžné verze položky.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-114">If the flag is not specified, prerelease items will not be shown.</span></span>
- <span data-ttu-id="2e7ce-115">Verze skriptu zobrazí Find-Script, Get-InstalledScript a v galerii prostředí PowerShell se zobrazí s PrereleaseString, stejně jako v 2.5.0-alpha.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-115">Script versions displayed by Find-Script, Get-InstalledScript, and in the PowerShell Gallery will be displayed with the PrereleaseString, as in 2.5.0-alpha.</span></span>

<span data-ttu-id="2e7ce-116">Podrobnosti o funkcích jsou uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-116">Details for the features are included below.</span></span>

## <a name="identifying-a-script-version-as-a-prerelease"></a><span data-ttu-id="2e7ce-117">Určení verze skriptu jako zkušební verze</span><span class="sxs-lookup"><span data-stu-id="2e7ce-117">Identifying a script version as a prerelease</span></span>

<span data-ttu-id="2e7ce-118">Podpora Správce balíčků PowerShellGet pro předběžné verze je snazší pro skripty než moduly.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-118">PowerShellGet support for prerelease versions is easier for scripts than modules.</span></span> <span data-ttu-id="2e7ce-119">Skript správy verzí je podporována pouze PowerShellGet, takže nejsou žádné problémy s kompatibilitou způsobila přidáním předběžné verze řetězce.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-119">Script versioning is only supported by PowerShellGet, so there are no compatibility issues caused by adding the prerelease string.</span></span> <span data-ttu-id="2e7ce-120">K identifikaci skript v galerii prostředí PowerShell jako zkušební verze, přidáte příponu předběžné verze správně formátovaný řetězec ve skriptu s metadaty.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-120">To identify a script in the PowerShell Gallery as a prerelease, add a prerelease suffix to a properly-formatted version string in the script metadata.</span></span>

<span data-ttu-id="2e7ce-121">Vzorový oddíl manifestu skript s předběžnou verzi by vypadat nějak takto:</span><span class="sxs-lookup"><span data-stu-id="2e7ce-121">An example section of a script manifest with a prerelease version would look like the following:</span></span>

```powershell
<#PSScriptInfo

.VERSION 3.2.1-alpha12

.GUID

...

#>
```

<span data-ttu-id="2e7ce-122">Pokud chcete použít příponu předběžné verze, řetězec verze musí splňovat následující požadavky:</span><span class="sxs-lookup"><span data-stu-id="2e7ce-122">To use a prerelease suffix, the version string must meet the following requirements:</span></span>

- <span data-ttu-id="2e7ce-123">Příponu předběžné verze jde zadat jenom když je verze 3 segmenty Major.Minor.Build.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-123">A prerelease suffix may only be specified when the Version is 3 segments for Major.Minor.Build.</span></span>
  <span data-ttu-id="2e7ce-124">Ten je v souladu s SemVer v1.0.0</span><span class="sxs-lookup"><span data-stu-id="2e7ce-124">This aligns with SemVer v1.0.0</span></span>
- <span data-ttu-id="2e7ce-125">Předběžné verze přípona je řetězec, který začíná spojovníkem a může obsahovat alfanumerické znaky ASCII [0-9A-Za - z-]</span><span class="sxs-lookup"><span data-stu-id="2e7ce-125">The prerelease suffix is a string which begins with a hyphen, and may contain ASCII alphanumerics [0-9A-Za-z-]</span></span>
- <span data-ttu-id="2e7ce-126">Jsou podporovány pouze řetězce předběžnou verzi v1.0.0 SemVer v tuto chvíli tak příponu předběžné verze **nesmí** obsahovat buď období nebo + [. +], které jsou povoleny v SemVer 2.0</span><span class="sxs-lookup"><span data-stu-id="2e7ce-126">Only SemVer v1.0.0 prerelease strings are supported at this time, so the prerelease suffix **must not** contain either period or + [.+], which are allowed in SemVer 2.0</span></span>
- <span data-ttu-id="2e7ce-127">Příklady podporovaných řetězců PrereleaseString:-alfa, - α1,-BETA, - update20171020</span><span class="sxs-lookup"><span data-stu-id="2e7ce-127">Examples of supported PrereleaseString strings are: -alpha, -alpha1, -BETA, -update20171020</span></span>

### <a name="prerelease-versioning-impact-on-sort-order-and-installation-folders"></a><span data-ttu-id="2e7ce-128">Předběžné verze správy verzí dopad na složky instalace a pořadí řazení</span><span class="sxs-lookup"><span data-stu-id="2e7ce-128">Prerelease versioning impact on sort order and installation folders</span></span>

<span data-ttu-id="2e7ce-129">Pořadí řazení se změní při používání předběžné verze, což je důležité při publikování do Galerie prostředí PowerShell, a při instalaci skriptů pomocí příkazů PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-129">Sort order changes when using a prerelease version, which is important when publishing to the PowerShell Gallery, and when installing scripts using PowerShellGet commands.</span></span> <span data-ttu-id="2e7ce-130">Pokud dva skripty verze s číslem verze neexistuje, pořadí řazení je podle následující spojovník část řetězce.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-130">If two scripts versions with the version number exist, the sort order is based on the string portion following the hyphen.</span></span> <span data-ttu-id="2e7ce-131">Ano 2.5.0-alpha verze je menší než 2.5.0-beta, což je míň než 2.5.0-gamma.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-131">So, version 2.5.0-alpha is less than 2.5.0-beta, which is less than 2.5.0-gamma.</span></span> <span data-ttu-id="2e7ce-132">Pokud dva skripty mají stejné číslo verze a pouze jeden má PrereleaseString, skript **bez** příponu předběžné verze se předpokládá se, že verze připravené pro produkční prostředí a budou seřazeny jako větší než zkušební verze verze.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-132">If two scripts have the same version number, and only one has a PrereleaseString, the script **without** the prerelease suffix is assumed to be the production-ready version and will be sorted as a greater version than the prerelease version.</span></span> <span data-ttu-id="2e7ce-133">Jako příklad, když porovnání uvolní 2.5.0 a 2.5.0-beta, 2.5.0 verzi se budou považovat za větší z nich.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-133">As an example, when comparing releases 2.5.0 and 2.5.0-beta, the 2.5.0 version will be considered the greater of the two.</span></span>

<span data-ttu-id="2e7ce-134">Při publikování do Galerie prostředí PowerShell, ve výchozím nastavení verzi publikován skriptu musí mít s vyšší verzí, než všechny dříve publikované verzi, která je v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-134">When publishing to the PowerShell Gallery, by default the version of the script being published must have a greater version than any previously-published version that is in the PowerShell Gallery.</span></span> <span data-ttu-id="2e7ce-135">Vydavatel může aktualizovat verzi 2.5.0-alpha 2.5.0-beta nebo s 2.5.0 (s příponou žádné předběžné verze).</span><span class="sxs-lookup"><span data-stu-id="2e7ce-135">A publisher may update version 2.5.0-alpha with 2.5.0-beta, or with 2.5.0 (with no prerelease suffix).</span></span>

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a><span data-ttu-id="2e7ce-136">Hledání a získávání předběžnou verzi položky pomocí příkazů PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="2e7ce-136">Finding and acquiring prerelease items using PowerShellGet commands</span></span>

<span data-ttu-id="2e7ce-137">Práce s předběžnou verzi položky pomocí Správce balíčků PowerShellGet Find-Script, Install-Script aktualizace skriptu, a příkazy Save-Script vyžaduje přidání příznaku - AllowPrerelease.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-137">Dealing with prerelease items using PowerShellGet Find-Script, Install-Script, Update-Script, and Save-Script commands requires adding the -AllowPrerelease flag.</span></span> <span data-ttu-id="2e7ce-138">Pokud - AllowPrerelease není zadána, předběžné verze položky budou zahrnuty v případě, že jsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-138">If -AllowPrerelease is specified, prerelease items will be included if they are present.</span></span> <span data-ttu-id="2e7ce-139">Pokud se nezadá příznak - AllowPrerelease, nezobrazí se předběžné verze položky.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-139">If -AllowPrerelease flag is not specified, prerelease items will not be shown.</span></span>

<span data-ttu-id="2e7ce-140">Jedinou výjimkou tohoto v příkazy skriptu PowerShellGet jsou Get-InstalledScript a někdy se skript pro odinstalaci.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-140">The only exceptions to this in the PowerShellGet script commands are Get-InstalledScript, and some cases with Uninstall-Script.</span></span>

- <span data-ttu-id="2e7ce-141">Get-InstalledScript vždy automaticky zobrazí informace o předběžnou verzi v řetězci verze pokud je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-141">Get-InstalledScript always will automatically show the prerelease information in the version string if it is present.</span></span>
- <span data-ttu-id="2e7ce-142">Odinstalovat skriptu bude ve výchozím nastavení odinstalace nejnovější verzi skriptu, pokud **žádná verze** je zadán.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-142">Uninstall-Script will by default uninstall the most recent version of a script, if **no version** is specified.</span></span> <span data-ttu-id="2e7ce-143">Aby nedošlo ke změně chování.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-143">That behavior has not changed.</span></span> <span data-ttu-id="2e7ce-144">Nicméně pokud předprodejní verze určena pomocí `-RequiredVersion`, `-AllowPrerelease` se bude vyžadovat.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-144">However, if a prerelease version is specified using `-RequiredVersion`, `-AllowPrerelease` will be required.</span></span>

## <a name="examples"></a><span data-ttu-id="2e7ce-145">Příklady</span><span class="sxs-lookup"><span data-stu-id="2e7ce-145">Examples</span></span>

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

<span data-ttu-id="2e7ce-146">Odinstalovat skript odebere aktuální verzi skriptu, pokud není zadán - RequiredVersion.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-146">Uninstall-Script will remove the current version of a script when -RequiredVersion is not supplied.</span></span>
<span data-ttu-id="2e7ce-147">Pokud je zadán - RequiredVersion a je zkušební verze, - AllowPrerelease musí přidat k příkazu.</span><span class="sxs-lookup"><span data-stu-id="2e7ce-147">If -RequiredVersion is specified, and is a prerelease, -AllowPrerelease must be added to the command.</span></span>

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

## <a name="more-details"></a><span data-ttu-id="2e7ce-148">Další podrobnosti</span><span class="sxs-lookup"><span data-stu-id="2e7ce-148">More details</span></span>

- [<span data-ttu-id="2e7ce-149">Verze předběžnou verzi modulu</span><span class="sxs-lookup"><span data-stu-id="2e7ce-149">Prerelease Module Versions</span></span>](module-prerelease-support.md)
- [<span data-ttu-id="2e7ce-150">Find-script</span><span class="sxs-lookup"><span data-stu-id="2e7ce-150">Find-script</span></span>](/powershell/module/powershellget/find-script)
- [<span data-ttu-id="2e7ce-151">Instalační skript</span><span class="sxs-lookup"><span data-stu-id="2e7ce-151">Install-script</span></span>](/powershell/module/powershellget/install-script)
- [<span data-ttu-id="2e7ce-152">Save-script</span><span class="sxs-lookup"><span data-stu-id="2e7ce-152">Save-script</span></span>](/powershell/module/powershellget/save-script)
- [<span data-ttu-id="2e7ce-153">Skript pro aktualizaci</span><span class="sxs-lookup"><span data-stu-id="2e7ce-153">Update-script</span></span>](/powershell/module/powershellget/update-script)
- [<span data-ttu-id="2e7ce-154">Get-Installedscript</span><span class="sxs-lookup"><span data-stu-id="2e7ce-154">Get-Installedscript</span></span>](/powershell/module/powershellget/get-installedscript)
- [<span data-ttu-id="2e7ce-155">Odinstalace script</span><span class="sxs-lookup"><span data-stu-id="2e7ce-155">UnInstall-script</span></span>](/powershell/module/powershellget/uninstall-script)