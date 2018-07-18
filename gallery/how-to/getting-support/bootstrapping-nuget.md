---
ms.date: 06/12/2017
contributor: manikb
keywords: Galerie prostředí powershell, rutina, psget
title: Probíhá spuštění NuGet
ms.openlocfilehash: 2d321097fda201c0d8f843b2194a161eceabe4e1
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39094013"
---
# <a name="bootstrap-the-nuget-provider-and-nugetexe"></a><span data-ttu-id="66f68-103">Bootstrap, NuGet zprostředkovatele a NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="66f68-103">Bootstrap the NuGet provider and NuGet.exe</span></span>

<span data-ttu-id="66f68-104">NuGet.exe není součástí nejnovějšího zprostředkovatele NuGet.</span><span class="sxs-lookup"><span data-stu-id="66f68-104">NuGet.exe is not included in the latest NuGet provider.</span></span>
<span data-ttu-id="66f68-105">Pro publikování operací modulu nebo skriptu, modulu PowerShellGet vyžaduje binární NuGet.exe spustitelný soubor.</span><span class="sxs-lookup"><span data-stu-id="66f68-105">For publish operations of either a module or script, PowerShellGet requires the binary executable NuGet.exe.</span></span>
<span data-ttu-id="66f68-106">Jen pro NuGet se vyžaduje pro všechny ostatní operace, včetně *najít*, *nainstalovat*, *Uložit*, a *odinstalovat*.</span><span class="sxs-lookup"><span data-stu-id="66f68-106">Only the NuGet provider is required for all other operations, including *find*, *install*, *save*, and *uninstall*.</span></span>
<span data-ttu-id="66f68-107">Správce balíčků PowerShellGet zahrnuje logiky, která by buď kombinované bootstrap, NuGet zprostředkovatele a NuGet.exe nebo bootstrap jediný poskytovatel NuGet.</span><span class="sxs-lookup"><span data-stu-id="66f68-107">PowerShellGet includes logic to handle either a combined bootstrap of the NuGet provider and NuGet.exe, or bootstrap of only the NuGet provider.</span></span>
<span data-ttu-id="66f68-108">V obou případech se budou objevovat pouze jedna zpráva příkazový řádek.</span><span class="sxs-lookup"><span data-stu-id="66f68-108">In either case, only a single prompt message should occur.</span></span>
<span data-ttu-id="66f68-109">Pokud počítač není připojený k Internetu, uživatel nebo správce musíte zkopírovat instanci důvěryhodného zprostředkovatele NuGet a/nebo soubor NuGet.exe odpojeném počítači.</span><span class="sxs-lookup"><span data-stu-id="66f68-109">If the machine is not connected to the Internet, the user or an administrator must copy a trusted instance of the NuGet provider and/or the NuGet.exe file to the disconnected machine.</span></span>

> [!NOTE]
> <span data-ttu-id="66f68-110">Od verze 6, NuGet poskytovatel je součástí instalace prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66f68-110">Starting with version 6, the NuGet provider is included in the installation of PowerShell.</span></span> [http://github.com/powershell/powershell](http://github.com/powershell/powershell)

## <a name="resolving-error-when-the-nuget-provider-has-not-been-installed-on-a-machine-that-is-internet-connected"></a><span data-ttu-id="66f68-111">Řešení chyby při NuGet zprostředkovatel nebyl nainstalován na počítači, který je internetové připojení</span><span class="sxs-lookup"><span data-stu-id="66f68-111">Resolving error when the NuGet provider has not been installed on a machine that is Internet connected</span></span>

```powershell
Find-Module -Repository PSGallery -Verbose -Name Contoso
```

```output
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
```

```powershell
Find-Module -Repository PSGallery -Verbose -Name Contoso
```

```output
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

## <a name="resolving-error-when-the-nuget-provider-is-available-and-nugetexe-is-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a><span data-ttu-id="66f68-112">Řešení chyby, když je k dispozici poskytovatel NuGet a NuGet.exe není k dispozici během operace publikování na počítači, který je Internet připojení</span><span class="sxs-lookup"><span data-stu-id="66f68-112">Resolving error when the NuGet provider is available and NuGet.exe is not available during the publish operation on a machine that is Internet connected</span></span>

```powershell
Publish-Module -Name Contoso -Repository PSGallery -Verbose
```

```output
NuGet.exe is required to continue
PowerShellGet requires NuGet.exe to publish an item to the NuGet-based repositories. NuGet.exe must be available under one of the paths specified in PATH environment variable value. Do you want PowerShellGet to install NuGet.exe now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): N
Publish-Module : NuGet.exe is required to interact with NuGet-based repositories. Please ensure that NuGet.exe is available under one of the paths specified in PATH environment variable value.
At line:1 char:1
+ Publish-Module -Name Contoso -Repository PSGallery -Verbose
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Publish-Module], InvalidOperationException
    + FullyQualifiedErrorId : CouldNotInstallNuGetExe,Publish-Module
```

```powershell
Publish-Module -Name Contoso -Repository PSGallery -Verbose
```

```output
NuGet.exe is required to continue
PowerShellGet requires NuGet.exe to publish an item to the NuGet-based repositories. NuGet.exe must be available under one of the paths specified in PATH environment variable value. Do you want PowerShellGet to install NuGet.exe now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet.exe.
VERBOSE: Successfully published module 'Contoso' to the module publish location 'https://www.powershellgallery.com/api/v2/'. Please allow few minutes for 'Contoso' to show up in the search results.
```

## <a name="resolving-error-when-both-nuget-provider-and-nugetexe-are-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a><span data-ttu-id="66f68-113">Řešení chyby, pokud poskytovatel NuGet a NuGet.exe nejsou k dispozici během operace publikování na počítači, který je Internet připojení</span><span class="sxs-lookup"><span data-stu-id="66f68-113">Resolving error when both NuGet provider and NuGet.exe are not available during the publish operation on a machine that is Internet connected</span></span>

```powershell
Publish-Module -Name Contoso -Repository PSGallery -Verbose
```

```output
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
```

```powershell
Publish-Module -Name Contoso -Repository PSGallery -Verbose
```

```output
NuGet.exe and NuGet provider are required to continue
PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Do you want PowerShellGet to install both NuGet.exe and NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet provider.
VERBOSE: Installing NuGet.exe.
VERBOSE: Successfully published module 'Contoso' to the module publish location 'https://www.powershellgallery.com/api/v2/'. Please allow few minutes for 'Contoso' to show up in the search results.
```

## <a name="manually-bootstrapping-the-nuget-provider-on-a-machine-that-is-not-connected-to-the-internet"></a><span data-ttu-id="66f68-114">Ruční spuštění poskytovatele NuGet na počítač, který není připojený k Internetu</span><span class="sxs-lookup"><span data-stu-id="66f68-114">Manually bootstrapping the NuGet provider on a machine that is not connected to the Internet</span></span>

<span data-ttu-id="66f68-115">Procesy, které jsme vám ukázali výše předpokládají tento počítač je připojený k Internetu a může stáhnout soubory ze na veřejném místě.</span><span class="sxs-lookup"><span data-stu-id="66f68-115">The processes demonstrated above assume the machine is connected to the Internet and can download files from a public location.</span></span>
<span data-ttu-id="66f68-116">Pokud tento způsob není možný, je jedinou možností spuštění počítače pomocí výše uvedené procesy a ručně zkopírujete do izolovaný uzel prostřednictvím offline proces důvěryhodného zprostředkovatele.</span><span class="sxs-lookup"><span data-stu-id="66f68-116">If that is not possible, the only option is to bootstrap a machine using the processes given above, and manually copy the provider to the isolated node through an offline trusted process.</span></span>
<span data-ttu-id="66f68-117">Nejběžnější případ použití pro tento scénář je, když je k dispozici pro podporu prostředí izolované privátní galerie.</span><span class="sxs-lookup"><span data-stu-id="66f68-117">The most common use case for this scenario is when a private gallery is available to support an isolated environment.</span></span>

<span data-ttu-id="66f68-118">Po provedení postupu výše bootstrap počítač připojený k Internetu, najdete v umístění soubory zprostředkovatele:</span><span class="sxs-lookup"><span data-stu-id="66f68-118">After following the process above to bootstrap an Internet connected machine, you will find provider files in the location:</span></span>

```
C:\Program Files\PackageManagement\ProviderAssemblies\
```

<span data-ttu-id="66f68-119">Struktura složky nebo souboru NuGet poskytovatele bude (případně s jinou verzi číslo):</span><span class="sxs-lookup"><span data-stu-id="66f68-119">The folder/file structure of the NuGet provider will be (possibly with a different version number):</span></span>

```
NuGet
--2.8.5.208
----Microsoft.PackageManagement.NuGetProvider.dll
```

<span data-ttu-id="66f68-120">Zkopírujte tyto složky a souboru pomocí důvěryhodného procesu do počítače offline.</span><span class="sxs-lookup"><span data-stu-id="66f68-120">Copy these folders and file using a trusted process to the offline machines.</span></span>

## <a name="manually-bootstrapping-nugetexe-to-support-publish-operations-on-a-machine-that-is-not-connected-to-the-internet"></a><span data-ttu-id="66f68-121">Ruční spuštění NuGet.exe pro podporu operací na počítači, který není připojen k Internetu publikování</span><span class="sxs-lookup"><span data-stu-id="66f68-121">Manually bootstrapping NuGet.exe to support publish operations on a machine that is not connected to the Internet</span></span>

<span data-ttu-id="66f68-122">Kromě proces ručně bootstrap poskytovatele NuGet, pokud je počítač se použije k privátní Galerie pomocí publikování moduly nebo skripty `Publish-Module` nebo `Publish-Script` rutin NuGet.exe binárního spustitelného souboru se bude vyžadovat.</span><span class="sxs-lookup"><span data-stu-id="66f68-122">In addition to the process to manually bootstrap the NuGet provider, if the machine will be used to publish modules or scripts to a private gallery using the `Publish-Module` or `Publish-Script` cmdlets, the NuGet.exe binary executable file will be required.</span></span>

<span data-ttu-id="66f68-123">Nejběžnější případ použití pro tento scénář je, když je k dispozici pro podporu prostředí izolované privátní galerie.</span><span class="sxs-lookup"><span data-stu-id="66f68-123">The most common use case for this scenario is when a private gallery is available to support an isolated environment.</span></span>
<span data-ttu-id="66f68-124">Existují dvě možnosti, jak získat soubor NuGet.exe.</span><span class="sxs-lookup"><span data-stu-id="66f68-124">There are two options to obtain the NuGet.exe file.</span></span>

<span data-ttu-id="66f68-125">Jednou z možností je spustit počítači, který je připojených k Internetu a zkopírujte soubory do počítače offline pomocí důvěryhodného procesu.</span><span class="sxs-lookup"><span data-stu-id="66f68-125">One option is to bootstrap a machine that is Internet connected and copy the files to the offline machines using a trusted process.</span></span>
<span data-ttu-id="66f68-126">Po spuštění počítač připojený Internet, budou umístěny binární NuGet.exe v jednom z dvě složky:</span><span class="sxs-lookup"><span data-stu-id="66f68-126">After bootstrapping the Internet connected machine, the NuGet.exe binary will be located in one of two folders:</span></span>

<span data-ttu-id="66f68-127">Pokud `Publish-Module` nebo `Publish-Script` rutiny byly prováděn se zvýšenými oprávněními (jako správce):</span><span class="sxs-lookup"><span data-stu-id="66f68-127">If the `Publish-Module` or `Publish-Script` cmdlets were executed with elevated permissions (As an Administrator):</span></span>

```powershell
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

<span data-ttu-id="66f68-128">Pokud rutiny bylo provedeno jako uživatel bez zvýšenou úroveň oprávnění:</span><span class="sxs-lookup"><span data-stu-id="66f68-128">If the cmdlets were executed as a user without elevated permissions:</span></span>

```powershell
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```

<span data-ttu-id="66f68-129">Druhou možností je můžete stáhnout z webu NuGet.Org NuGet.exe: [ https://dist.nuget.org/index.html ](https://www.nuget.org/downloads) při výběru verze Nuget pro počítače v produkčním prostředí, ujistěte se, že je pozdější než 2.8.5.208 a identifikovat verzi, která má s popiskem " Doporučené".</span><span class="sxs-lookup"><span data-stu-id="66f68-129">A second option is to download NuGet.exe from the NuGet.Org website: [https://dist.nuget.org/index.html](https://www.nuget.org/downloads) When selecting a NugGet version for production machines, make sure it is later than 2.8.5.208, and identify the version that has been labeled "recommended".</span></span>
<span data-ttu-id="66f68-130">Mějte na paměti odblokujete soubor, pokud byl stažen z prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="66f68-130">Remember to unblock the file if it was downloaded using a browser.</span></span>
<span data-ttu-id="66f68-131">Můžete to provést pomocí `Unblock-File` rutiny.</span><span class="sxs-lookup"><span data-stu-id="66f68-131">This can be performed by using the `Unblock-File` cmdlet.</span></span>

<span data-ttu-id="66f68-132">V obou případech se soubor NuGet.exe je možné zkopírovat do libovolného umístění v `$env:path`, ale standardní umístění jsou:</span><span class="sxs-lookup"><span data-stu-id="66f68-132">In either case, the NuGet.exe file can be copied to any location in `$env:path`, but the standard locations are:</span></span>

<span data-ttu-id="66f68-133">Spustitelný soubor zpřístupnit tak, aby všichni uživatelé můžou používat `Publish-Module` a `Publish-Script` rutiny:</span><span class="sxs-lookup"><span data-stu-id="66f68-133">To make the executable available so that all users can use `Publish-Module` and `Publish-Script` cmdlets:</span></span>

```powershell
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

<span data-ttu-id="66f68-134">Chcete-li spustitelný soubor k dispozici pro konkrétního uživatele, zkopírujte do umístění v rámci pouze profil daného uživatele:</span><span class="sxs-lookup"><span data-stu-id="66f68-134">To make the executable available to only a specific user, copy to the location within only that user's profile:</span></span>

```powershell
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```