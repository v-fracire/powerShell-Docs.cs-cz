---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: Zavedení spouštěcího programu NuGet zprostředkovatele a EXE
ms.openlocfilehash: 1c8d99491aec6d2a598facb909c1f36f4bb979e7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="bootstrap-both-nuget-provider-and-nugetexe-or-bootstrap-only-nuget-provider"></a><span data-ttu-id="8c4d3-103">Bootstrap NuGet poskytovatele i NuGet.exe nebo bootstrap pouze NuGet zprostředkovatele</span><span class="sxs-lookup"><span data-stu-id="8c4d3-103">Bootstrap both NuGet provider and NuGet.exe or bootstrap only NuGet provider</span></span>

<span data-ttu-id="8c4d3-104">NuGet.exe není zahrnutý ve zprostředkovateli nejnovější NuGet.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-104">NuGet.exe is not included in the latest NuGet provider.</span></span>
<span data-ttu-id="8c4d3-105">Pro publikování operace modul nebo skriptu, PowerShellGet vyžaduje binární NuGet.exe spustitelný soubor.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-105">For publish operations of either a module or script, PowerShellGet requires the binary executable NuGet.exe.</span></span>
<span data-ttu-id="8c4d3-106">Pouze NuGet se vyžaduje pro všechny ostatní operace, včetně *najít*, *nainstalovat*, *Uložit*, a *odinstalovat*.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-106">Only the NuGet provider is required for all other operations, including *find*, *install*, *save*, and *uninstall*.</span></span>
<span data-ttu-id="8c4d3-107">PowerShellGet obsahuje logiku pro zpracování buď kombinované bootstrap zprostředkovatele NuGet a NuGet.exe nebo bootstrap pouze zprostředkovatele NuGet.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-107">PowerShellGet includes logic to handle either a combined bootstrap of the NuGet provider and NuGet.exe, or bootstrap of only the NuGet provider.</span></span>
<span data-ttu-id="8c4d3-108">V obou případech pouze jeden řádek zpráva se může zobrazit.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-108">In either case, only a single prompt message should occur.</span></span>
<span data-ttu-id="8c4d3-109">Pokud počítač není připojený k Internetu, uživatel nebo správce musí zkopírovat důvěryhodné instanci zprostředkovatele NuGet nebo soubor NuGet.exe odpojené počítače.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-109">If the machine is not connected to the Internet, the user or an administrator must copy a trusted instance of the NuGet provider and/or the NuGet.exe file to the disconnected machine.</span></span>

><span data-ttu-id="8c4d3-110">**Poznámka:**: od verze 6 zprostředkovatele NuGet je součástí instalace prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-110">**Note**: Starting with version 6, the NuGet provider is included in the installation of PowerShell.</span></span> [http://github.com/powershell/powershell](http://github.com/powershell/powershell)

## <a name="resolving-error-when-the-nuget-provider-has-not-been-installed-on-a-machine-that-is-internet-connected"></a><span data-ttu-id="8c4d3-111">Řešení chyby, pokud zprostředkovatel NuGet nebyl nainstalován v počítači, ve kterém je Internet připojení</span><span class="sxs-lookup"><span data-stu-id="8c4d3-111">Resolving error when the NuGet provider has not been installed on a machine that is Internet connected</span></span>

```powershell
PS C:\> Find-Module -Repository PSGallery -Verbose -Name Contoso

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\manikb\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the NuGet provider
now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): n
Find-Module : NuGet provider is required to interact with NuGet-based repositories. Please ensure that '2.8.5.201' or newer version of NuGet provider is installed.
At line:1 char:1
+ Find-Module -Repository PSGallery -Verbose -Name Contoso
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Find-Module], InvalidOperationException
   + FullyQualifiedErrorId : CouldNotInstallNuGetProvider,Find-Module

PS C:\> Find-Module -Repository PSGallery -Verbose -Name Contoso

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\manikb\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the NuGet provider
now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet provider.

Version    Name                                Type       Repository           Description
-------    ----                                ----       ----------           -----------
2.5        Contoso                             Module     PSGallery        Contoso module
```
## <a name="resolving-error-when-the-nuget-provider-is-available-and-nugetexe-is-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a><span data-ttu-id="8c4d3-112">Řešení chyby, pokud je k dispozici zprostředkovatel NuGet a NuGet.exe není k dispozici na počítači, který je v Internetu během publikování připojení</span><span class="sxs-lookup"><span data-stu-id="8c4d3-112">Resolving error when the NuGet provider is available and NuGet.exe is not available during the publish operation on a machine that is Internet connected</span></span>

```powershell
PS C:\> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe is required to continue
PowerShellGet requires NuGet.exe to publish an item to the NuGet-based repositories. NuGet.exe must be available under one of the paths specified in PATH environment variable value. Do you want PowerShellGet to install NuGet.exe now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): N
Publish-Module : NuGet.exe is required to interact with NuGet-based repositories. Please ensure that NuGet.exe is available under one of the paths specified in PATH environment variable value.
At line:1 char:1
+ Publish-Module -Name Contoso -Repository PSGallery -Verbose
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Publish-Module], InvalidOperationException
    + FullyQualifiedErrorId : CouldNotInstallNuGetExe,Publish-Module

PS C:\> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe is required to continue
PowerShellGet requires NuGet.exe to publish an item to the NuGet-based repositories. NuGet.exe must be available under one of the paths specified in PATH environment variable value. Do you want PowerShellGet to install NuGet.exe now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet.exe.
VERBOSE: Successfully published module 'Contoso' to the module publish location 'https://www.powershellgallery.com/api/v2/'. Please allow few minutes for 'Contoso' to show up in the search results.
```

## <a name="resolving-error-when-both-nuget-provider-and-nugetexe-are-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a><span data-ttu-id="8c4d3-113">Řešení chyby, pokud zprostředkovatel NuGet a NuGet.exe nejsou k dispozici na počítači, který je v Internetu během publikování připojení</span><span class="sxs-lookup"><span data-stu-id="8c4d3-113">Resolving error when both NuGet provider and NuGet.exe are not available during the publish operation on a machine that is Internet connected</span></span>

```powershell
PS C:\> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe and NuGet provider are required to continue
PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Do you want PowerShellGet to install both NuGet.exe and NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): N
Publish-Module : PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Please ensure that '2.8.5.201' or newer version of NuGet provider is installed and NuGet.exe is available under
one of the paths specified in PATH environment variable value.
At line:1 char:1
+ Publish-Module -Name Contoso -Repository PSGallery -Verbose
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Publish-Module], InvalidOperationException
    + FullyQualifiedErrorId : CouldNotInstallNuGetBinaries,Publish-Module

PS C:\> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe and NuGet provider are required to continue
PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Do you want PowerShellGet to install both NuGet.exe and NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet provider.
VERBOSE: Installing NuGet.exe.
VERBOSE: Successfully published module 'Contoso' to the module publish location 'https://www.powershellgallery.com/api/v2/'. Please allow few minutes for 'Contoso' to show up in the search results.
```

## <a name="manually-bootstrapping-the-nuget-provider-on-a-machine-that-is-not-connected-to-the-internet"></a><span data-ttu-id="8c4d3-114">Ručně zavádění NuGet zprostředkovatele na počítači, který není připojený k Internetu</span><span class="sxs-lookup"><span data-stu-id="8c4d3-114">Manually bootstrapping the NuGet provider on a machine that is not connected to the Internet</span></span>

<span data-ttu-id="8c4d3-115">Procesy ukázán výše předpokládají tento počítač je připojený k Internetu a může stáhnout soubory z na veřejném místě.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-115">The processes demonstrated above assume the machine is connected to the Internet and can download files from a public location.</span></span>
<span data-ttu-id="8c4d3-116">Pokud tento způsob není možný, je jedinou možností bootstrap počítače, pomocí výše uvedené procesy a ručně zkopírovat do uzlu izolované offline proces důvěryhodného zprostředkovatele.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-116">If that is not possible, the only option is to bootstrap a machine using the processes given above, and manually copy the provider to the isolated node through an offline trusted process.</span></span>
<span data-ttu-id="8c4d3-117">Nejběžnější případ použití pro tento scénář je-li k dispozici pro podporu prostředí izolované privátní galerie.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-117">The most common use case for this scenario is when a private gallery is available to support an isolated environment.</span></span>

<span data-ttu-id="8c4d3-118">Až projdete proces výše a bootstrap počítač připojený Internetu, zjistíte zprostředkovatele soubory v umístění:</span><span class="sxs-lookup"><span data-stu-id="8c4d3-118">After following the process above to bootstrap an Internet connected machine, you will find provider files in the location:</span></span>
```
C:\Program Files\PackageManagement\ProviderAssemblies\
```

<span data-ttu-id="8c4d3-119">Struktura složka či soubor zprostředkovatele NuGet bude (případně s číslem různé verze):</span><span class="sxs-lookup"><span data-stu-id="8c4d3-119">The folder/file structure of the NuGet provider will be (possibly with a different version number):</span></span>

<span data-ttu-id="8c4d3-120">NuGet</span><span class="sxs-lookup"><span data-stu-id="8c4d3-120">NuGet</span></span><br>
<span data-ttu-id="8c4d3-121">--2.8.5.208</span><span class="sxs-lookup"><span data-stu-id="8c4d3-121">--2.8.5.208</span></span><br>
<span data-ttu-id="8c4d3-122">----Microsoft.PackageManagement.NuGetProvider.dll</span><span class="sxs-lookup"><span data-stu-id="8c4d3-122">----Microsoft.PackageManagement.NuGetProvider.dll</span></span>

<span data-ttu-id="8c4d3-123">Zkopírujte tyto složky a souboru pomocí důvěryhodného procesu na počítače, do režimu offline.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-123">Copy these folders and file using a trusted process to the offline machines.</span></span>

## <a name="manually-bootstrapping-nugetexe-to-support-publish-operations-on-a-machine-that-is-not-connected-to-the-internet"></a><span data-ttu-id="8c4d3-124">Ručně zavádění NuGet.exe pro podporu operací na počítači, který není připojený k Internetu publikování</span><span class="sxs-lookup"><span data-stu-id="8c4d3-124">Manually bootstrapping NuGet.exe to support publish operations on a machine that is not connected to the Internet</span></span>

<span data-ttu-id="8c4d3-125">Kromě proces ručně bootstrap NuGet poskytovatele, pokud je počítač bude používat k publikování moduly nebo skripty k privátní Galerie pomocí *publikovat modulu* nebo *publikovat skriptu* rutin binární spustitelný soubor NuGet.exe bude požadován.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-125">In addition to the process to manually bootstrap the NuGet provider, if the machine will be used to publish modules or scripts to a private gallery using the *Publish-Module* or *Publish-Script* cmdlets, the NuGet.exe binary executable file will be required.</span></span>
<span data-ttu-id="8c4d3-126">Nejběžnější případ použití pro tento scénář je-li k dispozici pro podporu prostředí izolované privátní galerie.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-126">The most common use case for this scenario is when a private gallery is available to support an isolated environment.</span></span>
<span data-ttu-id="8c4d3-127">Existují dvě možnosti získání NuGet.exe souboru.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-127">There are two options to obtain the NuGet.exe file.</span></span>

<span data-ttu-id="8c4d3-128">Jednou z možností je bootstrap počítač, který je internetové připojení a zkopírujte soubory do offline počítače pomocí důvěryhodného procesu.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-128">One option is to bootstrap a machine that is Internet connected and copy the files to the offline machines using a trusted process.</span></span>
<span data-ttu-id="8c4d3-129">Po zavedení spouštěcího programu připojený počítač Internet, budou umístěny binární NuGet.exe v jednom z dvě složky:</span><span class="sxs-lookup"><span data-stu-id="8c4d3-129">After bootstrapping the Internet connected machine, the NuGet.exe binary will be located in one of two folders:</span></span>

<span data-ttu-id="8c4d3-130">Pokud *publikovat modulu* nebo *publikovat skriptu* rutiny měla provést se zvýšenými oprávněními (jako správce):</span><span class="sxs-lookup"><span data-stu-id="8c4d3-130">If the *Publish-Module* or *Publish-Script* cmdlets were executed with elevated permissions (As an Administrator):</span></span>
```
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

<span data-ttu-id="8c4d3-131">Pokud rutiny měla provést jako uživatel bez zvýšenými oprávněními:</span><span class="sxs-lookup"><span data-stu-id="8c4d3-131">If the cmdlets were executed as a user without elevated permissions:</span></span>
```
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```

<span data-ttu-id="8c4d3-132">Druhou možností je stáhnout z webu NuGet.Org NuGet.exe: [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)</span><span class="sxs-lookup"><span data-stu-id="8c4d3-132">A second option is to download NuGet.exe from the NuGet.Org website: [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)</span></span><br>
<span data-ttu-id="8c4d3-133">Když vyberete verze Nuget pro produkčního počítače, ujistěte se, že je novější než 2.8.5.208 a identifikovat verzi, která označené "doporučené".</span><span class="sxs-lookup"><span data-stu-id="8c4d3-133">When selecting a NugGet version for production machines, make sure it is later than 2.8.5.208, and identify the version that has been labeled "recommended".</span></span>
<span data-ttu-id="8c4d3-134">Mějte na paměti, chcete-li odblokovat soubor, pokud byl stažen pomocí prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-134">Remember to unblock the file if it was downloaded using a browser.</span></span>
<span data-ttu-id="8c4d3-135">To lze provést pomocí *odblokovat soubor* rutiny.</span><span class="sxs-lookup"><span data-stu-id="8c4d3-135">This can be performed by using the *Unblock-File* cmdlet.</span></span>

<span data-ttu-id="8c4d3-136">V obou případech lze zkopírovat soubor NuGet.exe na libovolné místo v *$env: cesta*, ale jsou standardní umístění:</span><span class="sxs-lookup"><span data-stu-id="8c4d3-136">In either case, the NuGet.exe file can be copied to any location in *$env:path*, but the standard locations are:</span></span>

<span data-ttu-id="8c4d3-137">Chcete zpřístupnit spustitelný soubor, aby všichni uživatelé používat *publikovat modulu* a *publikovat skriptu* rutiny:</span><span class="sxs-lookup"><span data-stu-id="8c4d3-137">To make the executable available so that all users can use *Publish-Module* and *Publish-Script* cmdlets:</span></span>
```
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

<span data-ttu-id="8c4d3-138">Spustitelný soubor zpřístupnit pro konkrétního uživatele, zkopírujte do umístění v rámci pouze tento uživatel profilu:</span><span class="sxs-lookup"><span data-stu-id="8c4d3-138">To make the executable available to only a specific user, copy to the location within only that user's profile:</span></span>
```
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```