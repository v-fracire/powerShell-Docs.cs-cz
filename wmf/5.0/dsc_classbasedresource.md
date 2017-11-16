---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: d40e5475c4132d6377c9a4559262a41b4842180a
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="class-based-dsc-resources"></a><span data-ttu-id="17113-102">Prostředky založené na třídě DSC</span><span class="sxs-lookup"><span data-stu-id="17113-102">Class-based DSC Resources</span></span>

## <a name="defining-dsc-resources-with-classes"></a><span data-ttu-id="17113-103">Definování prostředky DSC s třídami</span><span class="sxs-lookup"><span data-stu-id="17113-103">Defining DSC resources with classes</span></span>

<span data-ttu-id="17113-104">Na základě názorů, jsme provedli jsme vytváření založené na třídě jednodušší a srozumitelnější prostředky DSC.</span><span class="sxs-lookup"><span data-stu-id="17113-104">Based on feedback, we’ve made authoring class-based DSC resources simpler and easier to understand.</span></span> <span data-ttu-id="17113-105">Hlavní rozdíly mezi prostředek DSC založené na třídě a poskytovatel prostředků DSC rutiny jsou:</span><span class="sxs-lookup"><span data-stu-id="17113-105">The major differences between a class-based DSC resource and a cmdlet DSC resource provider are:</span></span>

* <span data-ttu-id="17113-106">Soubor MOF pro schéma se nevyžaduje.</span><span class="sxs-lookup"><span data-stu-id="17113-106">A MOF file for the schema is not required.</span></span>
* <span data-ttu-id="17113-107">A **DSCResource** podsložky ve složce modulu se nevyžaduje.</span><span class="sxs-lookup"><span data-stu-id="17113-107">A **DSCResource** subfolder in the module folder is not required.</span></span>
* <span data-ttu-id="17113-108">Soubor modulu prostředí PowerShell může obsahovat několik tříd prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="17113-108">A PowerShell module file can contain multiple DSC resource classes.</span></span>

<span data-ttu-id="17113-109">Další informace najdete v tématu [zápis vlastní prostředek DSC pomocí prostředí PowerShell třídy](https://msdn.microsoft.com/powershell/dsc/authoringresource).</span><span class="sxs-lookup"><span data-stu-id="17113-109">For more information, see [Writing a custom DSC resource with PowerShell classes](https://msdn.microsoft.com/powershell/dsc/authoringresource).</span></span>

