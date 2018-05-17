---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 0543afbc72148b1ba713e59655126c069b16ef33
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="side-by-side-module-versioning-support-for-dsc-resources"></a>Podpora vedle sebe modulu Správa verzí pro prostředky DSC

Moduly obsahující prostředky DSC mohou být nainstalovány souběžně sdílená a konfigurace DSC můžete použít konkrétní verzi prostředku, který je v systému nainstalována.

Další informace najdete v tématu [pomocí prostředků s více verzemi](https://msdn.microsoft.com/powershell/dsc/sxsresource).

## <a name="known-issues"></a>Známé problémy

V této verzi následující seznam uvádí známé problémy instalace vedle sebe:

-   Použití dvě různé verze prostředek DSC v rámci stejné konfigurace není podporováno.
