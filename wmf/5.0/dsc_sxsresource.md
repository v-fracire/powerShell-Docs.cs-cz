---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 0543afbc72148b1ba713e59655126c069b16ef33
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="side-by-side-module-versioning-support-for-dsc-resources"></a><span data-ttu-id="0084b-102">Podpora vedle sebe modulu Správa verzí pro prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="0084b-102">Side-By-Side Module Versioning Support for DSC Resources</span></span>

<span data-ttu-id="0084b-103">Moduly obsahující prostředky DSC mohou být nainstalovány souběžně sdílená a konfigurace DSC můžete použít konkrétní verzi prostředku, který je v systému nainstalována.</span><span class="sxs-lookup"><span data-stu-id="0084b-103">Modules containing DSC resources can be installed side-by-side, and DSC configurations can use a specific version of the resource that is installed on the system.</span></span>

<span data-ttu-id="0084b-104">Další informace najdete v tématu [pomocí prostředků s více verzemi](https://msdn.microsoft.com/powershell/dsc/sxsresource).</span><span class="sxs-lookup"><span data-stu-id="0084b-104">For more information, see [Using resources with multiple versions](https://msdn.microsoft.com/powershell/dsc/sxsresource).</span></span>

## <a name="known-issues"></a><span data-ttu-id="0084b-105">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="0084b-105">Known issues</span></span>

<span data-ttu-id="0084b-106">V této verzi následující seznam uvádí známé problémy instalace vedle sebe:</span><span class="sxs-lookup"><span data-stu-id="0084b-106">In this release, the following are known issues of side-by-side installation:</span></span>

-   <span data-ttu-id="0084b-107">Použití dvě různé verze prostředek DSC v rámci stejné konfigurace není podporováno.</span><span class="sxs-lookup"><span data-stu-id="0084b-107">Using two different versions of the DSC resource within the same configuration is not supported.</span></span>
