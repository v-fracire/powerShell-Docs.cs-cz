---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: b839b476bb4ef7f8d73b158d61f0e8cbc1265e60
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="import-dscresource-keyword-supports--moduleversion-parameter"></a><span data-ttu-id="ab89b-102">Parametr - ModuleVersion podporuje import DscResource – klíčové slovo</span><span class="sxs-lookup"><span data-stu-id="ab89b-102">Import-DscResource keyword supports -ModuleVersion parameter</span></span>

<span data-ttu-id="ab89b-103">Jsme přidali nový parametr, který se `Import-DscResource` dynamické – klíčové slovo dostupné při vytváření konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="ab89b-103">We have added a new parameter to the `Import-DscResource` dynamic keyword available when authoring DSC configurations.</span></span> <span data-ttu-id="ab89b-104">Autoři konfigurace nyní můžete určit přesně verze načíst prostředky DSC z které modulu.</span><span class="sxs-lookup"><span data-stu-id="ab89b-104">Configuration authors can now specify exactly which module version to load the DSC resources from.</span></span> <span data-ttu-id="ab89b-105">Nové syntaxe klíčového slova je:</span><span class="sxs-lookup"><span data-stu-id="ab89b-105">The new syntax of the keyword is:</span></span>

```powershell
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>] [-ModuleVersion <ModuleVersion>]
```

* <span data-ttu-id="ab89b-106">**Název**: názvy jeden nebo více prostředků pro import.</span><span class="sxs-lookup"><span data-stu-id="ab89b-106">**Name**: Names of one or more resources to import.</span></span>
* <span data-ttu-id="ab89b-107">**Název modulu**: názvy modulů nebo ModuleSpecification objekty jeden nebo více modulů pro import.</span><span class="sxs-lookup"><span data-stu-id="ab89b-107">**ModuleName**: Module names or ModuleSpecification objects of one or more modules to import.</span></span>
* <span data-ttu-id="ab89b-108">**Verze modulu**: verzi importu typ objektu modulu.</span><span class="sxs-lookup"><span data-stu-id="ab89b-108">**ModuleVersion**: Version of module ot import.</span></span> <span data-ttu-id="ab89b-109">Pokud se používá, název modulu musí představovat pouze jeden modul podle názvu.</span><span class="sxs-lookup"><span data-stu-id="ab89b-109">If used, ModuleName must represent only one module by name.</span></span> 

<span data-ttu-id="ab89b-110">V systému Windows PowerShell ISE se zobrazí s IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="ab89b-110">In the Windows PowerShell ISE, it shows up with IntelliSense:</span></span>

![](../images/Import-DscResource-Modversion.jpg)

<span data-ttu-id="ab89b-111">**Poznámka:**: `–ModuleVersion` parametr lze použít pouze v kombinaci s `–ModuleName` parametr.</span><span class="sxs-lookup"><span data-stu-id="ab89b-111">**Note**: the `–ModuleVersion` parameter can only be used in combination with the `–ModuleName` parameter.</span></span> <span data-ttu-id="ab89b-112">Nedá se použít s názvy prostředků pomocí pouze `–Name` parametr.</span><span class="sxs-lookup"><span data-stu-id="ab89b-112">It cannot be used with resource names using only the `–Name` parameter.</span></span>

<span data-ttu-id="ab89b-113">Před tím jediný způsob, jak při načítání prostředků DSC určit verze modulu byl pomocí specifikace objektu modulu. například:`–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`</span><span class="sxs-lookup"><span data-stu-id="ab89b-113">Before this, the only way to specify the module version when loading DSC resources was by using the Module specification object e.g.: `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`</span></span>

