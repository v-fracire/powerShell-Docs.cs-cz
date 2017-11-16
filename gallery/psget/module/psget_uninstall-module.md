---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: Odinstalujte modul
ms.openlocfilehash: 3c4d8faa63aba6b4434d42a19a219baf84122591
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="uninstall-module"></a><span data-ttu-id="c7a1e-103">Odinstalujte modul</span><span class="sxs-lookup"><span data-stu-id="c7a1e-103">Uninstall-Module</span></span>

<span data-ttu-id="c7a1e-104">Odinstaluje modul, který byl nainstalován pomocí rutin PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="c7a1e-104">Uninstalls a module which was installed using PowerShellGet cmdlets.</span></span>

## <a name="description"></a><span data-ttu-id="c7a1e-105">Popis</span><span class="sxs-lookup"><span data-stu-id="c7a1e-105">Description</span></span>

<span data-ttu-id="c7a1e-106">Rutina Uninstall-Module odinstaluje zadaný modul z místního počítače.</span><span class="sxs-lookup"><span data-stu-id="c7a1e-106">The Uninstall-Module cmdlet uninstalls the specified module from the local computer.</span></span> <span data-ttu-id="c7a1e-107">Modul nelze odinstalovat, pokud některé z ostatních modulů jsou závislé na něm.</span><span class="sxs-lookup"><span data-stu-id="c7a1e-107">You cannot uninstall a module if some other modules have a dependency on it.</span></span>
<span data-ttu-id="c7a1e-108">Rutiny Uninstall-Module zároveň ověří, pokud modul Probíhá odinstalace je používán, nebo ne.</span><span class="sxs-lookup"><span data-stu-id="c7a1e-108">The Uninstall-Module cmdlets also validates if the module being uninstalled is in-use or not.</span></span> <span data-ttu-id="c7a1e-109">Pokud modul se používá, bude vyvolána chyba.</span><span class="sxs-lookup"><span data-stu-id="c7a1e-109">An error will be thrown if the module is in use.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="c7a1e-110">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="c7a1e-110">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Uninstall-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="c7a1e-111">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="c7a1e-111">Cmdlet online help reference</span></span>

[<span data-ttu-id="c7a1e-112">Odinstalujte modul</span><span class="sxs-lookup"><span data-stu-id="c7a1e-112">Uninstall-Module</span></span>](http://go.microsoft.com/fwlink/?LinkId=526864)


## <a name="example-commands"></a><span data-ttu-id="c7a1e-113">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="c7a1e-113">Example commands</span></span>

###  <a name="run-the-uninstall-module-cmdlet-to-uninstall-a-module-that-you-installed-by-using-powershellget"></a><span data-ttu-id="c7a1e-114">Spusťte rutinu Uninstall-Module odinstalovat modul, který jste nainstalovali pomocí PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="c7a1e-114">Run the Uninstall-Module cmdlet to uninstall a module that you installed by using PowerShellGet.</span></span>
<span data-ttu-id="c7a1e-115">Pokud ostatní moduly závisí na modul, který chcete odstranit, PowerShellGet vrátí chybu.</span><span class="sxs-lookup"><span data-stu-id="c7a1e-115">If any other module depends on the module that you want to delete, PowerShellGet throws an error.</span></span>
```powershell
Get-InstalledModule -Name RequiredModule1 | Uninstall-Module

PackageManagement\Uninstall-Package : The module 'RequiredModule1' of version '2.5' in module base folder 'C:\Program Files\WindowsPowerShell\Modules\RequiredModule1\2.5' cannot be uninstalled, because one or more other modules 'ModuleWithDependencies2' are dependent on this module. Uninstall the modules that depend on this module before uninstalling module 'RequiredModule1'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\PSGet.psm1:1303 char:25
+ ... $null = PackageManagement\\Uninstall-Package @PSBoundParameters
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo : InvalidOperation: (Microsoft.Power...ninstallPackage:UninstallPackage) [Uninstall-Package], Exception
+ FullyQualifiedErrorId : UnableToUninstallAsOtherModulesNeedThisModule,Uninstall-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.UninstallPackage
```

### <a name="uninstalling-a-module-when-some-other-modules-have-a-dependency-on-it"></a><span data-ttu-id="c7a1e-116">Odinstalování modul, když některé z ostatních modulů jsou závislé na něm.</span><span class="sxs-lookup"><span data-stu-id="c7a1e-116">Uninstalling a module when some other modules have a dependency on it.</span></span>

```powershell
Uninstall-Module SnippetPx

PackageManagement\Uninstall-Package : The module 'SnippetPx' of version '1.0.5.18' in module base folder 'C:\ProgramFiles\WindowsPowerShell\Modules\SnippetPx\1.0.5.18' cannot be uninstalled, because one or more other modules 'TypePx' are dependent on this module. Uninstall the modules that depend on this module before uninstalling module 'SnippetPx'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.3\PSModule.psm1:1803 char:21
+ ...        $null = PackageManagement\Uninstall-Package @PSBoundParameters
+                    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (Microsoft.Power...ninstallPackage:UninstallPackage) [Uninstall-Packag
   e], Exception
    + FullyQualifiedErrorId : UnableToUninstallAsOtherModulesNeedThisModule,Uninstall-Package,Microsoft.PowerShell.Pac
   kageManagement.Cmdlets.UninstallPackage
```

### <a name="you-can-override-this-by-specify--force-option-on-uninstall-module-cmdlet"></a><span data-ttu-id="c7a1e-117">Toto můžete přepsat pomocí zadejte - Force – možnost o rutině Uninstall-Module</span><span class="sxs-lookup"><span data-stu-id="c7a1e-117">You can override this by specify -Force option on Uninstall-Module cmdlet</span></span>
<span data-ttu-id="c7a1e-118">**Poznámka:** toto není doporučený postup.</span><span class="sxs-lookup"><span data-stu-id="c7a1e-118">**NOTE:** This is not a recommended practice.</span></span> <span data-ttu-id="c7a1e-119">Pomocí této akce dojde k přerušení ostatních modulů.</span><span class="sxs-lookup"><span data-stu-id="c7a1e-119">Other modules will break with this action.</span></span>

```powershell
Uninstall-Module SnippetPx -Force
```

### <a name="uninstall-a-module-which-is-already-in-use"></a><span data-ttu-id="c7a1e-120">Odinstalujte modul, který je již používán</span><span class="sxs-lookup"><span data-stu-id="c7a1e-120">Uninstall a module which is already in use</span></span>

```powershell
Get-InstalledModule TypePx,SnippetPx

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.0.1.20   TypePx                              PSGallery            The TypePx module adds properties and methods to...
1.0.5.18   SnippetPx                           PSGallery            The SnippetPx module enhances the snippet experi...
```

### <a name="uninstall-snippetpx-fails-due-to-the-dependent-module"></a><span data-ttu-id="c7a1e-121">Odinstalace SnippetPx nezdaří z důvodu závislé modulu</span><span class="sxs-lookup"><span data-stu-id="c7a1e-121">Uninstall SnippetPx fails due to the dependent module</span></span>

```powershell
Uninstall-Module SnippetPx

PackageManagement\Uninstall-Package : The module 'SnippetPx' of version '1.0.5.18' in module base folder 'C:\Program
Files\WindowsPowerShell\Modules\SnippetPx\1.0.5.18' cannot be uninstalled, because one or more other modules 'TypePx'
are dependent on this module. Uninstall the modules that depend on this module before uninstalling module 'SnippetPx'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1914 char:21
+ ...        $null = PackageManagement\Uninstall-Package @PSBoundParameters
+                    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (Microsoft.Power...ninstallPackage:UninstallPackage) [Uninstall-Packag
   e], Exception
    + FullyQualifiedErrorId : UnableToUninstallAsOtherModulesNeedThisModule,Uninstall-Package,Microsoft.PowerShell.Pac
   kageManagement.Cmdlets.UninstallPackage
```

### <a name="uninstall-typepx-then-uninstall-the-snippetpx"></a><span data-ttu-id="c7a1e-122">Odinstalace TypePx pak odinstalujte SnippetPx</span><span class="sxs-lookup"><span data-stu-id="c7a1e-122">Uninstall TypePx then uninstall the SnippetPx</span></span>

```powershell
Uninstall-Module TypePx
Uninstall-Module SnippetPx

WARNING: The version '1.0.5.18' of module 'SnippetPx' is currently in use. Retry the operation after closing the
applications.
PackageManagement\Uninstall-Package : Module 'SnippetPx' is in currently in use.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1914 char:21
+ ...        $null = PackageManagement\Uninstall-Package @PSBoundParameters
+                    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (Microsoft.Power...ninstallPackage:UninstallPackage) [Uninstall-Packag
   e], Exception
    + FullyQualifiedErrorId : ModuleIsInUse,Uninstall-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.Uninstall
   Package
```


### <a name="for-a-module-name-which-is-not-installed-using-powershellget-cmdlets"></a><span data-ttu-id="c7a1e-123">Pro název modulu, který není nainstalován pomocí rutin PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="c7a1e-123">For a module name which is not installed using PowerShellGet cmdlets</span></span>

```powershell
Uninstall-Module SnipptPx

PackageManagement\Uninstall-Package : No match was found for the specified search criteria and module names 'SnipptPx'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1914 char:21
+ ...        $null = PackageManagement\Uninstall-Package @PSBoundParameters
+                    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...ninstallPackage:UninstallPackage) [Uninstall-Package]
   , Exception
    + FullyQualifiedErrorId : NoMatchFound,Microsoft.PowerShell.PackageManagement.Cmdlets.UninstallPackage
```

