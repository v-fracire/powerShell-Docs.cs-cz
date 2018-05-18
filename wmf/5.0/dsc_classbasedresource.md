---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 42f323590609319388e9a0a2c7c305dfa80c2d49
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="class-based-dsc-resources"></a><span data-ttu-id="fc8c3-102">Prostředky DSC založené na třídě</span><span class="sxs-lookup"><span data-stu-id="fc8c3-102">Class-based DSC Resources</span></span>

## <a name="defining-dsc-resources-with-classes"></a><span data-ttu-id="fc8c3-103">Definování prostředky DSC s třídami</span><span class="sxs-lookup"><span data-stu-id="fc8c3-103">Defining DSC resources with classes</span></span>

<span data-ttu-id="fc8c3-104">Na základě názorů, jsme provedli jsme vytváření založené na třídě jednodušší a srozumitelnější prostředky DSC.</span><span class="sxs-lookup"><span data-stu-id="fc8c3-104">Based on feedback, we’ve made authoring class-based DSC resources simpler and easier to understand.</span></span>
<span data-ttu-id="fc8c3-105">Hlavní rozdíly mezi prostředek DSC založené na třídě a poskytovatel prostředků DSC rutiny jsou:</span><span class="sxs-lookup"><span data-stu-id="fc8c3-105">The major differences between a class-based DSC resource and a cmdlet DSC resource provider are:</span></span>

* <span data-ttu-id="fc8c3-106">Soubor MOF pro schéma se nevyžaduje.</span><span class="sxs-lookup"><span data-stu-id="fc8c3-106">A MOF file for the schema is not required.</span></span>
* <span data-ttu-id="fc8c3-107">A **DSCResource** podsložky ve složce modulu se nevyžaduje.</span><span class="sxs-lookup"><span data-stu-id="fc8c3-107">A **DSCResource** subfolder in the module folder is not required.</span></span>
* <span data-ttu-id="fc8c3-108">Soubor modulu prostředí PowerShell může obsahovat několik tříd prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="fc8c3-108">A PowerShell module file can contain multiple DSC resource classes.</span></span>

<span data-ttu-id="fc8c3-109">Další informace najdete v tématu [zápis vlastní prostředek DSC pomocí prostředí PowerShell třídy](https://msdn.microsoft.com/powershell/dsc/authoringresource).</span><span class="sxs-lookup"><span data-stu-id="fc8c3-109">For more information, see [Writing a custom DSC resource with PowerShell classes](https://msdn.microsoft.com/powershell/dsc/authoringresource).</span></span>
