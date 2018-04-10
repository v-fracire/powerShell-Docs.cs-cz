---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: a3b176101bebf7081febd8629bddcfa0ae1e7540
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="import-dscresource-keyword-supports--moduleversion-parameter"></a><span data-ttu-id="6730c-102">Parametr - ModuleVersion podporuje import DscResource – klíčové slovo</span><span class="sxs-lookup"><span data-stu-id="6730c-102">Import-DscResource keyword supports -ModuleVersion parameter</span></span>

<span data-ttu-id="6730c-103">Jsme přidali nový parametr, který se `Import-DscResource` dynamické – klíčové slovo dostupné při vytváření konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="6730c-103">We have added a new parameter to the `Import-DscResource` dynamic keyword available when authoring DSC configurations.</span></span> <span data-ttu-id="6730c-104">Autoři konfigurace nyní můžete určit přesně verze načíst prostředky DSC z které modulu.</span><span class="sxs-lookup"><span data-stu-id="6730c-104">Configuration authors can now specify exactly which module version to load the DSC resources from.</span></span> <span data-ttu-id="6730c-105">Nové syntaxe klíčového slova je:</span><span class="sxs-lookup"><span data-stu-id="6730c-105">The new syntax of the keyword is:</span></span>

```powershell
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>] [-ModuleVersion <ModuleVersion>]
```

* <span data-ttu-id="6730c-106">**Název**: názvy jeden nebo více prostředků pro import.</span><span class="sxs-lookup"><span data-stu-id="6730c-106">**Name**: Names of one or more resources to import.</span></span>
* <span data-ttu-id="6730c-107">**Název modulu**: názvy modulů nebo ModuleSpecification objekty jeden nebo více modulů pro import.</span><span class="sxs-lookup"><span data-stu-id="6730c-107">**ModuleName**: Module names or ModuleSpecification objects of one or more modules to import.</span></span>
* <span data-ttu-id="6730c-108">**Verze modulu**: verzi importu typ objektu modulu.</span><span class="sxs-lookup"><span data-stu-id="6730c-108">**ModuleVersion**: Version of module ot import.</span></span> <span data-ttu-id="6730c-109">Pokud se používá, název modulu musí představovat pouze jeden modul podle názvu.</span><span class="sxs-lookup"><span data-stu-id="6730c-109">If used, ModuleName must represent only one module by name.</span></span>

<span data-ttu-id="6730c-110">V systému Windows PowerShell ISE se zobrazí s IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="6730c-110">In the Windows PowerShell ISE, it shows up with IntelliSense:</span></span>

![](../images/Import-DscResource-Modversion.jpg)

<span data-ttu-id="6730c-111">**Poznámka:**: `–ModuleVersion` parametr lze použít pouze v kombinaci s `–ModuleName` parametr.</span><span class="sxs-lookup"><span data-stu-id="6730c-111">**Note**: the `–ModuleVersion` parameter can only be used in combination with the `–ModuleName` parameter.</span></span> <span data-ttu-id="6730c-112">Nedá se použít s názvy prostředků pomocí pouze `–Name` parametr.</span><span class="sxs-lookup"><span data-stu-id="6730c-112">It cannot be used with resource names using only the `–Name` parameter.</span></span>

<span data-ttu-id="6730c-113">Před tím jediný způsob, jak při načítání prostředků DSC určit verze modulu byl pomocí specifikace objektu modulu. například: `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`</span><span class="sxs-lookup"><span data-stu-id="6730c-113">Before this, the only way to specify the module version when loading DSC resources was by using the Module specification object e.g.: `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`</span></span>