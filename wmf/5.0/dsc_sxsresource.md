---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: a565f2befddc32f5088fa3e158f58d2dd78d41b4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="side-by-side-module-versioning-support-for-dsc-resources"></a>Podpora vedle sebe modulu Správa verzí pro prostředky DSC

Moduly obsahující prostředky DSC mohou být nainstalovány souběžně sdílená a konfigurace DSC můžete použít konkrétní verzi prostředku, který je v systému nainstalována.

Další informace najdete v tématu [pomocí prostředků s více verzemi](https://msdn.microsoft.com/powershell/dsc/sxsresource).

## <a name="known-issues"></a>Známé problémy

V této verzi následující seznam uvádí známé problémy instalace vedle sebe:

-   Použití dvě různé verze prostředek DSC v rámci stejné konfigurace není podporováno.