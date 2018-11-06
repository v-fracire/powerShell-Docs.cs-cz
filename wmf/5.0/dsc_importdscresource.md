---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 46a278b83edb9d8e3d75b0874603710d416be3b5
ms.sourcegitcommit: f4247d3f91d06ec392c4cd66921ce7d0456a2bd9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2018
ms.locfileid: "50998516"
---
# <a name="import-dscresource-keyword-supports--moduleversion-parameter"></a><span data-ttu-id="8586f-102">Klíčové slovo import-DscResource podporuje parametr - ModuleVersion</span><span class="sxs-lookup"><span data-stu-id="8586f-102">Import-DscResource keyword supports -ModuleVersion parameter</span></span>

<span data-ttu-id="8586f-103">Přidali jsme nový parametr pro `Import-DscResource` dynamické klíčové slovo dostupné při vytváření konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="8586f-103">We have added a new parameter to the `Import-DscResource` dynamic keyword available when authoring DSC configurations.</span></span> <span data-ttu-id="8586f-104">Konfigurace autoři teď můžete zadat přesně verze modulu se načíst prostředky DSC od.</span><span class="sxs-lookup"><span data-stu-id="8586f-104">Configuration authors can now specify exactly which module version to load the DSC resources from.</span></span> <span data-ttu-id="8586f-105">Nová syntaxe klíčového slova je následující:</span><span class="sxs-lookup"><span data-stu-id="8586f-105">The new syntax of the keyword is:</span></span>

```powershell
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>] [-ModuleVersion <ModuleVersion>]
```

* <span data-ttu-id="8586f-106">**Název**: názvy jeden nebo více prostředků k importu.</span><span class="sxs-lookup"><span data-stu-id="8586f-106">**Name**: Names of one or more resources to import.</span></span>
* <span data-ttu-id="8586f-107">**Název modulu**: názvy modulů nebo ModuleSpecification objekty jeden nebo více modulů k importu.</span><span class="sxs-lookup"><span data-stu-id="8586f-107">**ModuleName**: Module names or ModuleSpecification objects of one or more modules to import.</span></span>
* <span data-ttu-id="8586f-108">**ModuleVersion**: verze modulu k importu.</span><span class="sxs-lookup"><span data-stu-id="8586f-108">**ModuleVersion**: Version of module to import.</span></span> <span data-ttu-id="8586f-109">Pokud použijete, musí představovat název modulu pouze jeden modul podle názvu.</span><span class="sxs-lookup"><span data-stu-id="8586f-109">If used, ModuleName must represent only one module by name.</span></span>

<span data-ttu-id="8586f-110">V prostředí Windows PowerShell ISE zobrazí se s technologií IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="8586f-110">In the Windows PowerShell ISE, it shows up with IntelliSense:</span></span>

![](../images/Import-DscResource-Modversion.jpg)

<span data-ttu-id="8586f-111">**Poznámka:**: `–ModuleVersion` parametr lze použít pouze v kombinaci s `–ModuleName` parametru.</span><span class="sxs-lookup"><span data-stu-id="8586f-111">**Note**: the `–ModuleVersion` parameter can only be used in combination with the `–ModuleName` parameter.</span></span> <span data-ttu-id="8586f-112">Nelze zadat s použitím pouze názvy prostředků `–Name` parametru.</span><span class="sxs-lookup"><span data-stu-id="8586f-112">It cannot be used with resource names using only the `–Name` parameter.</span></span>

<span data-ttu-id="8586f-113">Před tím jediný způsob, jak určit verzi modulu při načítání prostředků DSC byla například pomocí specifikace objekt Module: `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`</span><span class="sxs-lookup"><span data-stu-id="8586f-113">Before this, the only way to specify the module version when loading DSC resources was by using the Module specification object e.g.: `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`</span></span>
