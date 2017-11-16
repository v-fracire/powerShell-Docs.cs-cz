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
# <a name="class-based-dsc-resources"></a>Prostředky založené na třídě DSC

## <a name="defining-dsc-resources-with-classes"></a>Definování prostředky DSC s třídami

Na základě názorů, jsme provedli jsme vytváření založené na třídě jednodušší a srozumitelnější prostředky DSC. Hlavní rozdíly mezi prostředek DSC založené na třídě a poskytovatel prostředků DSC rutiny jsou:

* Soubor MOF pro schéma se nevyžaduje.
* A **DSCResource** podsložky ve složce modulu se nevyžaduje.
* Soubor modulu prostředí PowerShell může obsahovat několik tříd prostředků DSC.

Další informace najdete v tématu [zápis vlastní prostředek DSC pomocí prostředí PowerShell třídy](https://msdn.microsoft.com/powershell/dsc/authoringresource).

