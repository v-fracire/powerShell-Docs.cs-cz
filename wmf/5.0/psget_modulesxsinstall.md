---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: f68847ba8292a277e464025c1baa17a5aa2752f5
ms.sourcegitcommit: 4ab9a86e47b6effe8fe22ebeb81e8fadff41d31c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2017
---
# <a name="side-by-side-version-support-on-powershell-50-or-newer"></a><span data-ttu-id="5160d-102">Podpora verzí vedle sebe na prostředí PowerShell 5.0 nebo novější</span><span class="sxs-lookup"><span data-stu-id="5160d-102">Side-by-Side Version Support on PowerShell 5.0 or newer</span></span>

<span data-ttu-id="5160d-103">Nyní je podpora verze modulu (SxS) vedle sebe v instalaci modulu, aktualizace modulu a publikovat modul rutin, které spustit v prostředí Windows PowerShell 5.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="5160d-103">There is now side-by-side (SxS) module version support in Install-Module, Update-Module, and Publish-Module cmdlets that run in Windows PowerShell 5.0 or newer.</span></span>
<span data-ttu-id="5160d-104">Také jsme přidali parametr - RequiredVersion pro rutinu Publish-Module určit verzi k publikování.</span><span class="sxs-lookup"><span data-stu-id="5160d-104">Also, we have added a -RequiredVersion parameter to the Publish-Module cmdlet to specify the version to be published.</span></span> <span data-ttu-id="5160d-105">Parametr Path teď podporuje základní cesta modulu se složkou verze.</span><span class="sxs-lookup"><span data-stu-id="5160d-105">The Path parameter now supports the module base path with the version folder.</span></span>

<span data-ttu-id="5160d-106">**Instalace modulu příklady:**</span><span class="sxs-lookup"><span data-stu-id="5160d-106">**Install-Module examples:**</span></span>
```powershell
Install-Module -Name PSScriptAnalyzer -RequiredVersion 1.1.0 -Repository PSGallery
Get-Module -ListAvailable -Name PSScriptAnalyzer | Format-List Name,Version,ModuleBase

Name : PSScriptAnalyzer
Version : 1.1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.0

Install-Module -Name PSScriptAnalyzer -RequiredVersion 1.1.1 -Repository PSGallery
Get-Module -ListAvailable -Name PSScriptAnalyzer | Format-List Name,Version,ModuleBase

Name       : PSScriptAnalyzer 
Version    : 1.1.1
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.1
Name       : PSScriptAnalyzer
Version    : 1.1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.0

Get-InstalledModule -Name PSScriptAnalyzer -AllVersions

Version    Name                                Type       Repository           Description            
-------    ----                                ----       ----------           -----------            
1.1.0      PSScriptAnalyzer                    Module     PSGallery            PSScriptAnalyzer provides script analysis... 
1.1.1      PSScriptAnalyzer                    Module     PSGallery            PSScriptAnalyzer provides script analysis...
```

