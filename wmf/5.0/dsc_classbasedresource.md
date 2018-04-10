---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 4def20aa95f66ab23c9eee575150bc3db02541d8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="class-based-dsc-resources"></a><span data-ttu-id="02d0f-102">Prostředky DSC založené na třídě</span><span class="sxs-lookup"><span data-stu-id="02d0f-102">Class-based DSC Resources</span></span>

## <a name="defining-dsc-resources-with-classes"></a><span data-ttu-id="02d0f-103">Definování prostředky DSC s třídami</span><span class="sxs-lookup"><span data-stu-id="02d0f-103">Defining DSC resources with classes</span></span>

<span data-ttu-id="02d0f-104">Na základě názorů, jsme provedli jsme vytváření založené na třídě jednodušší a srozumitelnější prostředky DSC.</span><span class="sxs-lookup"><span data-stu-id="02d0f-104">Based on feedback, we’ve made authoring class-based DSC resources simpler and easier to understand.</span></span>
<span data-ttu-id="02d0f-105">Hlavní rozdíly mezi prostředek DSC založené na třídě a poskytovatel prostředků DSC rutiny jsou:</span><span class="sxs-lookup"><span data-stu-id="02d0f-105">The major differences between a class-based DSC resource and a cmdlet DSC resource provider are:</span></span>

* <span data-ttu-id="02d0f-106">Soubor MOF pro schéma se nevyžaduje.</span><span class="sxs-lookup"><span data-stu-id="02d0f-106">A MOF file for the schema is not required.</span></span>
* <span data-ttu-id="02d0f-107">A **DSCResource** podsložky ve složce modulu se nevyžaduje.</span><span class="sxs-lookup"><span data-stu-id="02d0f-107">A **DSCResource** subfolder in the module folder is not required.</span></span>
* <span data-ttu-id="02d0f-108">Soubor modulu prostředí PowerShell může obsahovat několik tříd prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="02d0f-108">A PowerShell module file can contain multiple DSC resource classes.</span></span>

<span data-ttu-id="02d0f-109">Další informace najdete v tématu [zápis vlastní prostředek DSC pomocí prostředí PowerShell třídy](https://msdn.microsoft.com/powershell/dsc/authoringresource).</span><span class="sxs-lookup"><span data-stu-id="02d0f-109">For more information, see [Writing a custom DSC resource with PowerShell classes](https://msdn.microsoft.com/powershell/dsc/authoringresource).</span></span>