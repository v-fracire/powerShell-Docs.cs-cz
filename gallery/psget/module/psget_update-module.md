---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: Aktualizace modulu
ms.openlocfilehash: 343c296dad2a3df35f13393b3796a1d484f5f535
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="update-module"></a><span data-ttu-id="cb40e-103">Aktualizace modulu</span><span class="sxs-lookup"><span data-stu-id="cb40e-103">Update-Module</span></span>

<span data-ttu-id="cb40e-104">Stáhne a nainstaluje nejnovější verzi zadané moduly z online galerie do místního počítače.</span><span class="sxs-lookup"><span data-stu-id="cb40e-104">Downloads and installs the newest version of specified modules from an online gallery to the local computer.</span></span>

## <a name="description"></a><span data-ttu-id="cb40e-105">Popis</span><span class="sxs-lookup"><span data-stu-id="cb40e-105">Description</span></span>

<span data-ttu-id="cb40e-106">Rutinu Update-Module nainstaluje na novější verzi modul prostředí Windows PowerShell, který byl nainstalován z online galerie spuštěním instalace modulu v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="cb40e-106">The Update-Module cmdlet installs a newer version of a Windows PowerShell module that was installed from the online gallery by running Install-Module on the local computer.</span></span>

<span data-ttu-id="cb40e-107">Ve výchozím nastavení je nainstalovaná nejnovější verze zadaný modul k dispozici v online galerie, pokud nezadáte požadovaná verze.</span><span class="sxs-lookup"><span data-stu-id="cb40e-107">By default, the newest version of the specified module available in online gallery is installed, unless you specify a required version.</span></span> <span data-ttu-id="cb40e-108">Modul existující, nainstalované můžete aktualizovat tak, že zadáte název modulu; Aktualizace modulu vyhledá $env: PSModulePath pro modul, který chcete aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="cb40e-108">You can update an existing, installed module by specifying the name of the module; Update-Module searches $env:PSModulePath for the module that you want to update.</span></span>

<span data-ttu-id="cb40e-109">Spuštění aktualizace modul bez názvu parametru aktualizuje všechny moduly, které mohou být aktualizovány na místním počítači.</span><span class="sxs-lookup"><span data-stu-id="cb40e-109">Running Update-Module without the Name parameter updates all modules that can be updated on the local computer.</span></span>

### <a name="notes"></a><span data-ttu-id="cb40e-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="cb40e-110">Notes</span></span>

- <span data-ttu-id="cb40e-111">Tato rutina se spustí v prostředí Windows PowerShell 3.0 nebo novější verze prostředí Windows PowerShell na Windows 7 nebo Windows 2008 R2 a pozdějších verzích Windows.</span><span class="sxs-lookup"><span data-stu-id="cb40e-111">This cmdlet runs on Windows PowerShell 3.0 or later releases of Windows PowerShell, on Windows 7 or Windows 2008 R2 and later releases of Windows.</span></span>
- <span data-ttu-id="cb40e-112">Pokud modul, který můžete určit pomocí parametru název nebyl nainstalován pomocí instalace modulu, dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="cb40e-112">If the module that you specify with the Name parameter was not installed by using Install-Module, an error occurs.</span></span> <span data-ttu-id="cb40e-113">Aktualizace modulu lze spustit jen u moduly, které jste nainstalovali z online galerie spuštěním instalace modulu.</span><span class="sxs-lookup"><span data-stu-id="cb40e-113">You can only run Update-Module on modules that you installed from the online gallery by running Install-Module.</span></span>
- <span data-ttu-id="cb40e-114">Pokud aktualizace modul se pokusí aktualizovat binární soubory, které se používají, aktualizace modulu vrátí chybu, která identifikuje procesy problém a informuje uživatele, zopakujte akci aktualizace modulu po ukončení procesů.</span><span class="sxs-lookup"><span data-stu-id="cb40e-114">If Update-Module attempts to update binaries that are in use, Update-Module returns an error that identifies the problem processes, and informs the user to retry Update-Module after stopping the processes.</span></span>
- <span data-ttu-id="cb40e-115">PowerShell 5.0 nebo novější verze Pokud aktualizace modulu aktualizuje modul, přidá nejnovější (nebo zadaný) verzi modulu, takže starší a novějších verzí teď-souběžného ve stejném adresáři.</span><span class="sxs-lookup"><span data-stu-id="cb40e-115">On PowerShell 5.0 or newer versions, when Update-Module updates a module, it adds the latest (or specified) version of the module, so the older and newer versions are now side-by-side in the same directory.</span></span> <span data-ttu-id="cb40e-116">Je užitečné k vyslovení tak a k zobrazení příkladu výstupu z těchto příkazů.</span><span class="sxs-lookup"><span data-stu-id="cb40e-116">It would be useful to say so and to show an example of the output from these commands.</span></span>


## <a name="cmdlet-syntax"></a><span data-ttu-id="cb40e-117">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="cb40e-117">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Update-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="cb40e-118">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="cb40e-118">Cmdlet online help reference</span></span>

[<span data-ttu-id="cb40e-119">Aktualizace modulu</span><span class="sxs-lookup"><span data-stu-id="cb40e-119">Update-Module</span></span>](http://go.microsoft.com/fwlink/?LinkID=398576)


## <a name="example-commands"></a><span data-ttu-id="cb40e-120">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="cb40e-120">Example commands</span></span>

```powershell
PS C:\\windows\\system32> Update-Module -Name ContosoServer -RequiredVersion 1.5
PS C:\\windows\\system32> Get-Module -ListAvailable -Name ContosoServer | Format-List Name,Version,ModuleBase
Name : ContosoServer
Version : 2.0
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\2.0
Name : ContosoServer
Version : 1.5
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\1.5
Name : ContosoServer
Version : 1.0
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\1.0
PS C:\\windows\\system32> Get-InstalledModule
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer MSPSGallery ContosoServer module
1.5 ContosoServer MSPSGallery ContosoServer module
2.0 ContosoServer MSPSGallery ContosoServer module
PS C:\\windows\\system32> Update-Module -Name ContosoServer
PS C:\\windows\\system32> Get-Module -ListAvailable -Name ContosoServer | Format-List Name,Version,ModuleBase
Name : ContosoServer
Version : 2.8.1
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\2.8.1
Name : ContosoServer
Version : 2.0
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\2.0
Name : ContosoServer
Version : 1.5
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\1.5
Name : ContosoServer
Version : 1.0
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\1.0
PS C:\\windows\\system32> Get-InstalledModule
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer MSPSGallery ContosoServer module
1.5 ContosoServer MSPSGallery ContosoServer module
2.0 ContosoServer MSPSGallery ContosoServer module
2.8.1 ContosoServer MSPSGallery ContosoServer module
```


###  <a name="update-the-testdepwithnestedrequiredmodules1-module-with-dependencies"></a><span data-ttu-id="cb40e-121">Aktualizace modulu TestDepWithNestedRequiredModules1 se závislostmi.</span><span class="sxs-lookup"><span data-stu-id="cb40e-121">Update the TestDepWithNestedRequiredModules1 module with dependencies.</span></span>
```powershell
Find-Module -Name TestDepWithNestedRequiredModules1 -Repository LocalRepo -AllVersions

Version    Name                                Repository  Description
-------    ----                                ----------  -----------
1.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
2.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module

Update-Module -Name TestDepWithNestedRequiredModules1 -RequiredVersion 2.0
Get-InstalledModule

Version    Name                                Repository  Description
-------    ----                                ----------  -----------
1.0        NestedRequiredModule1               LocalRepo   NestedRequiredModule1 module
2.5        NestedRequiredModule2               LocalRepo   NestedRequiredModule2 module
2.0        NestedRequiredModule3               LocalRepo   NestedRequiredModule3 module
2.5        NestedRequiredModule3               LocalRepo   NestedRequiredModule3 module
1.0        RequiredModule1                     LocalRepo   RequiredModule1 module
2.5        RequiredModule2                     LocalRepo   RequiredModule2 module
2.0        RequiredModule3                     LocalRepo   RequiredModule3 module
2.5        RequiredModule3                     LocalRepo   RequiredModule3 module
1.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
2.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
```

