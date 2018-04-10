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
# <a name="bootstrap-both-nuget-provider-and-nugetexe-or-bootstrap-only-nuget-provider"></a>Bootstrap NuGet poskytovatele i NuGet.exe nebo bootstrap pouze NuGet zprostředkovatele

NuGet.exe není zahrnutý ve zprostředkovateli nejnovější NuGet.
Pro publikování operace modul nebo skriptu, PowerShellGet vyžaduje binární NuGet.exe spustitelný soubor.
Pouze NuGet se vyžaduje pro všechny ostatní operace, včetně *najít*, *nainstalovat*, *Uložit*, a *odinstalovat*.
PowerShellGet obsahuje logiku pro zpracování buď kombinované bootstrap zprostředkovatele NuGet a NuGet.exe nebo bootstrap pouze zprostředkovatele NuGet.
V obou případech pouze jeden řádek zpráva se může zobrazit.
Pokud počítač není připojený k Internetu, uživatel nebo správce musí zkopírovat důvěryhodné instanci zprostředkovatele NuGet nebo soubor NuGet.exe odpojené počítače.

>**Poznámka:**: od verze 6 zprostředkovatele NuGet je součástí instalace prostředí PowerShell. [http://github.com/powershell/powershell](http://github.com/powershell/powershell)

## <a name="resolving-error-when-the-nuget-provider-has-not-been-installed-on-a-machine-that-is-internet-connected"></a>Řešení chyby, pokud zprostředkovatel NuGet nebyl nainstalován v počítači, ve kterém je Internet připojení

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
## <a name="resolving-error-when-the-nuget-provider-is-available-and-nugetexe-is-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a>Řešení chyby, pokud je k dispozici zprostředkovatel NuGet a NuGet.exe není k dispozici na počítači, který je v Internetu během publikování připojení

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

## <a name="resolving-error-when-both-nuget-provider-and-nugetexe-are-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a>Řešení chyby, pokud zprostředkovatel NuGet a NuGet.exe nejsou k dispozici na počítači, který je v Internetu během publikování připojení

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

## <a name="manually-bootstrapping-the-nuget-provider-on-a-machine-that-is-not-connected-to-the-internet"></a>Ručně zavádění NuGet zprostředkovatele na počítači, který není připojený k Internetu

Procesy ukázán výše předpokládají tento počítač je připojený k Internetu a může stáhnout soubory z na veřejném místě.
Pokud tento způsob není možný, je jedinou možností bootstrap počítače, pomocí výše uvedené procesy a ručně zkopírovat do uzlu izolované offline proces důvěryhodného zprostředkovatele.
Nejběžnější případ použití pro tento scénář je-li k dispozici pro podporu prostředí izolované privátní galerie.

Až projdete proces výše a bootstrap počítač připojený Internetu, zjistíte zprostředkovatele soubory v umístění:
```
C:\Program Files\PackageManagement\ProviderAssemblies\
```

Struktura složka či soubor zprostředkovatele NuGet bude (případně s číslem různé verze):

NuGet<br>
--2.8.5.208<br>
----Microsoft.PackageManagement.NuGetProvider.dll

Zkopírujte tyto složky a souboru pomocí důvěryhodného procesu na počítače, do režimu offline.

## <a name="manually-bootstrapping-nugetexe-to-support-publish-operations-on-a-machine-that-is-not-connected-to-the-internet"></a>Ručně zavádění NuGet.exe pro podporu operací na počítači, který není připojený k Internetu publikování

Kromě proces ručně bootstrap NuGet poskytovatele, pokud je počítač bude používat k publikování moduly nebo skripty k privátní Galerie pomocí *publikovat modulu* nebo *publikovat skriptu* rutin binární spustitelný soubor NuGet.exe bude požadován.
Nejběžnější případ použití pro tento scénář je-li k dispozici pro podporu prostředí izolované privátní galerie.
Existují dvě možnosti získání NuGet.exe souboru.

Jednou z možností je bootstrap počítač, který je internetové připojení a zkopírujte soubory do offline počítače pomocí důvěryhodného procesu.
Po zavedení spouštěcího programu připojený počítač Internet, budou umístěny binární NuGet.exe v jednom z dvě složky:

Pokud *publikovat modulu* nebo *publikovat skriptu* rutiny měla provést se zvýšenými oprávněními (jako správce):
```
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

Pokud rutiny měla provést jako uživatel bez zvýšenými oprávněními:
```
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```

Druhou možností je stáhnout z webu NuGet.Org NuGet.exe: [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)<br>
Když vyberete verze Nuget pro produkčního počítače, ujistěte se, že je novější než 2.8.5.208 a identifikovat verzi, která označené "doporučené".
Mějte na paměti, chcete-li odblokovat soubor, pokud byl stažen pomocí prohlížeče.
To lze provést pomocí *odblokovat soubor* rutiny.

V obou případech lze zkopírovat soubor NuGet.exe na libovolné místo v *$env: cesta*, ale jsou standardní umístění:

Chcete zpřístupnit spustitelný soubor, aby všichni uživatelé používat *publikovat modulu* a *publikovat skriptu* rutiny:
```
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

Spustitelný soubor zpřístupnit pro konkrétního uživatele, zkopírujte do umístění v rámci pouze tento uživatel profilu:
```
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```