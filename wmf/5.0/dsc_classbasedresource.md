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
# <a name="class-based-dsc-resources"></a>Prostředky DSC založené na třídě

## <a name="defining-dsc-resources-with-classes"></a>Definování prostředky DSC s třídami

Na základě názorů, jsme provedli jsme vytváření založené na třídě jednodušší a srozumitelnější prostředky DSC.
Hlavní rozdíly mezi prostředek DSC založené na třídě a poskytovatel prostředků DSC rutiny jsou:

* Soubor MOF pro schéma se nevyžaduje.
* A **DSCResource** podsložky ve složce modulu se nevyžaduje.
* Soubor modulu prostředí PowerShell může obsahovat několik tříd prostředků DSC.

Další informace najdete v tématu [zápis vlastní prostředek DSC pomocí prostředí PowerShell třídy](https://msdn.microsoft.com/powershell/dsc/authoringresource).