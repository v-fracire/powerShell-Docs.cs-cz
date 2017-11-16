---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 2c7e718bc518b332cb4303ef73b1bf5c924ca471
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="powershell-module-discovery-install-and-inventory-with-powershellget"></a><span data-ttu-id="77c4f-102">Modul prostředí PowerShell zjišťování, instalace a inventáře s PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="77c4f-102">PowerShell Module Discovery, Install and Inventory with PowerShellGet</span></span>
 
<span data-ttu-id="77c4f-103">PowerShellGet je zahrnutá v této verzi WMF:</span><span class="sxs-lookup"><span data-stu-id="77c4f-103">PowerShellGet is included in this release of WMF:</span></span>
-   <span data-ttu-id="77c4f-104">Vyhledání modulu můžete filtrovat podle metadata modulu s parametrem - značky</span><span class="sxs-lookup"><span data-stu-id="77c4f-104">Find-Module can filter on module metadata with the -Tag parameter</span></span>
-   <span data-ttu-id="77c4f-105">Vyhledání modulu můžete filtrovat podle jazyka vyhledávání podle úložiště s parametrem - filtru</span><span class="sxs-lookup"><span data-stu-id="77c4f-105">Find-Module can filter on repository-specific search language with the -Filter parameter</span></span>
-   <span data-ttu-id="77c4f-106">Můžete najít modul filtr založený na modulu obsah s-příkazového - DscResource a - obsahuje parametry</span><span class="sxs-lookup"><span data-stu-id="77c4f-106">Find-Module can filter based on module contents with the -Command, -DscResource, and -Includes parameters</span></span>
-   <span data-ttu-id="77c4f-107">Umožňuje najít DscResource zjišťování jednotlivé prostředky DSC v úložiště</span><span class="sxs-lookup"><span data-stu-id="77c4f-107">Find-DscResource allows discovery of individual DSC resources in repositories</span></span>
-   <span data-ttu-id="77c4f-108">Podpora pro instalaci z a publikování do sdílené složky s NuGet</span><span class="sxs-lookup"><span data-stu-id="77c4f-108">Support for installing from and publishing to file shares with NuGet</span></span>

## <a name="example-commands"></a><span data-ttu-id="77c4f-109">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="77c4f-109">Example commands</span></span>
```powershell
\# Find all modules with tags Azure or DSC
Find-Module -Tag Azure, DSC

\# Find modules with a specific DscResource
Find-Module -DscResource xFirewall

\#Find modules with specific commands
Find-Module -Command Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

\# Find all modules with Dsc resources
Find-Module -Includes DscResource

\# Find all modules with cmdlets
Find-Module -Includes Cmdlet

\# Find all modules with functions
Find-Module -Includes Function

\# Find all DSC resources
Find-DscResource

\# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking

\# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

\# Find modules using -Filter parameter
\# Specified filter value is searched in Name and Description properties
Find-Module -Filter Cookbook -Repository PSGallery
Find-Module -Filter RBAC -Repository PSGallery
```

## <a name="new-features-in-powershellget"></a><span data-ttu-id="77c4f-110">Nové funkce v PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="77c4f-110">New features in PowerShellGet</span></span>
-   <span data-ttu-id="77c4f-111">Podpora verzí vedle sebe na prostředí Windows PowerShell 5.0 nebo novější</span><span class="sxs-lookup"><span data-stu-id="77c4f-111">Side-by-side version support on Windows PowerShell 5.0 or newer</span></span>
-   <span data-ttu-id="77c4f-112">Podpora instalace závislostí modulu</span><span class="sxs-lookup"><span data-stu-id="77c4f-112">Module dependency installation support</span></span>
-   <span data-ttu-id="77c4f-113">Tři nové rutiny</span><span class="sxs-lookup"><span data-stu-id="77c4f-113">Three new cmdlets</span></span>
    -   <span data-ttu-id="77c4f-114">Get-InstalledModule</span><span class="sxs-lookup"><span data-stu-id="77c4f-114">Get-InstalledModule</span></span>
    -   <span data-ttu-id="77c4f-115">Odinstalujte modul</span><span class="sxs-lookup"><span data-stu-id="77c4f-115">Uninstall-Module</span></span>
    -   <span data-ttu-id="77c4f-116">Uložit – modul</span><span class="sxs-lookup"><span data-stu-id="77c4f-116">Save-Module</span></span>
    
