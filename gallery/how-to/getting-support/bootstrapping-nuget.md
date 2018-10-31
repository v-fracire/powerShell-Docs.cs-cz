---
ms.date: 06/12/2017
contributor: manikb
keywords: Galerie prostředí powershell, rutina, psget
title: Probíhá spuštění NuGet
ms.openlocfilehash: 6d8f106bc3b8741203e87e4c097948a843f06d6e
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002134"
---
# <a name="bootstrap-the-nuget-provider-and-nugetexe"></a>Bootstrap, NuGet zprostředkovatele a NuGet.exe

NuGet.exe není součástí nejnovějšího zprostředkovatele NuGet. Pro publikování operací modulu nebo skriptu, modulu PowerShellGet vyžaduje binární NuGet.exe spustitelný soubor. Jen pro NuGet se vyžaduje pro všechny ostatní operace, včetně *najít*, *nainstalovat*, *Uložit*, a *odinstalovat*.
Správce balíčků PowerShellGet zahrnuje logiky, která by buď kombinované bootstrap, NuGet zprostředkovatele a NuGet.exe nebo bootstrap jediný poskytovatel NuGet. V obou případech se budou objevovat pouze jedna zpráva příkazový řádek. Pokud počítač není připojený k Internetu, uživatel nebo správce musíte zkopírovat instanci důvěryhodného zprostředkovatele NuGet a/nebo soubor NuGet.exe odpojeném počítači.

> [!NOTE]
> Od verze 6, NuGet poskytovatel je součástí instalace prostředí PowerShell.

## <a name="resolving-error-when-the-nuget-provider-has-not-been-installed-on-a-machine-that-is-internet-connected"></a>Řešení chyby při NuGet zprostředkovatel nebyl nainstalován na počítači, který je internetové připojení

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

## <a name="resolving-error-when-the-nuget-provider-is-available-and-nugetexe-is-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a>Řešení chyby, když je k dispozici poskytovatel NuGet a NuGet.exe není k dispozici během operace publikování na počítači, který je Internet připojení

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

## <a name="resolving-error-when-both-nuget-provider-and-nugetexe-are-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a>Řešení chyby, pokud poskytovatel NuGet a NuGet.exe nejsou k dispozici během operace publikování na počítači, který je Internet připojení

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

## <a name="manually-bootstrapping-the-nuget-provider-on-a-machine-that-is-not-connected-to-the-internet"></a>Ruční spuštění poskytovatele NuGet na počítač, který není připojený k Internetu

Procesy, které jsme vám ukázali výše předpokládají tento počítač je připojený k Internetu a může stáhnout soubory ze na veřejném místě. Pokud tento způsob není možný, je jedinou možností spuštění počítače pomocí výše uvedené procesy a ručně zkopírujete do izolovaný uzel prostřednictvím offline proces důvěryhodného zprostředkovatele. Nejběžnější případ použití pro tento scénář je, když je k dispozici pro podporu prostředí izolované privátní galerie.

Po provedení postupu výše bootstrap počítač připojený k Internetu, najdete v umístění soubory zprostředkovatele:

`C:\Program Files\PackageManagement\ProviderAssemblies\`

Struktura složky nebo souboru NuGet poskytovatele bude (případně s jinou verzi číslo):

```
NuGet
--2.8.5.208
----Microsoft.PackageManagement.NuGetProvider.dll
```

Zkopírujte tyto složky a souboru pomocí důvěryhodného procesu do počítače offline.

## <a name="manually-bootstrapping-nugetexe-to-support-publish-operations-on-a-machine-that-is-not-connected-to-the-internet"></a>Ruční spuštění NuGet.exe pro podporu operací na počítači, který není připojen k Internetu publikování

Kromě proces ručně bootstrap poskytovatele NuGet, pokud je počítač se použije k privátní Galerie pomocí publikování moduly nebo skripty `Publish-Module` nebo `Publish-Script` rutin NuGet.exe binárního spustitelného souboru se bude vyžadovat.

Nejběžnější případ použití pro tento scénář je, když je k dispozici pro podporu prostředí izolované privátní galerie. Existují dvě možnosti, jak získat soubor NuGet.exe.

Jednou z možností je spustit počítači, který je připojených k Internetu a zkopírujte soubory do počítače offline pomocí důvěryhodného procesu. Po spuštění počítač připojený Internet, budou umístěny binární NuGet.exe v jednom z dvě složky:

Pokud `Publish-Module` nebo `Publish-Script` rutiny byly prováděn se zvýšenými oprávněními (jako správce):

```powershell
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

Pokud rutiny bylo provedeno jako uživatel bez zvýšenou úroveň oprávnění:

```powershell
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```

Druhou možností je můžete stáhnout z webu NuGet.Org NuGet.exe: [ https://dist.nuget.org/index.html ](https://www.nuget.org/downloads) při výběru verze Nuget pro počítače v produkčním prostředí, ujistěte se, že je pozdější než 2.8.5.208 a identifikovat verzi, která má s popiskem " Doporučené". Mějte na paměti odblokujete soubor, pokud byl stažen z prohlížeče. Můžete to provést pomocí `Unblock-File` rutiny.

V obou případech se soubor NuGet.exe je možné zkopírovat do libovolného umístění v `$env:path`, ale standardní umístění jsou:

Spustitelný soubor zpřístupnit tak, aby všichni uživatelé můžou používat `Publish-Module` a `Publish-Script` rutiny:

```powershell
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

Chcete-li spustitelný soubor k dispozici pro konkrétního uživatele, zkopírujte do umístění v rámci pouze profil daného uživatele:

```powershell
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```
