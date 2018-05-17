---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 42f323590609319388e9a0a2c7c305dfa80c2d49
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="class-based-dsc-resources"></a>Prostředky DSC založené na třídě

## <a name="defining-dsc-resources-with-classes"></a>Definování prostředky DSC s třídami

Na základě názorů, jsme provedli jsme vytváření založené na třídě jednodušší a srozumitelnější prostředky DSC.
Hlavní rozdíly mezi prostředek DSC založené na třídě a poskytovatel prostředků DSC rutiny jsou:

* Soubor MOF pro schéma se nevyžaduje.
* A **DSCResource** podsložky ve složce modulu se nevyžaduje.
* Soubor modulu prostředí PowerShell může obsahovat několik tříd prostředků DSC.

Další informace najdete v tématu [zápis vlastní prostředek DSC pomocí prostředí PowerShell třídy](https://msdn.microsoft.com/powershell/dsc/authoringresource).
