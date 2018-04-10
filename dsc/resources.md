---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Prostředky DSC
ms.openlocfilehash: e393c8fe2e1ba8d68ba9aa1b656d1e5ebfad30e8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-resources"></a>Prostředky DSC

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Požadované prostředky konfigurace stavu (DSC) poskytují stavební bloky pro konfiguraci DSC. Prostředek zpřístupní vlastnosti, které může být nakonfigurované (schéma) a obsahuje funkce skriptu prostředí PowerShell, které místní Configuration Manager (LCM) žádostí na "jej tak".

Prostředek může model něco jako obecný jako soubor nebo co nastavení serveru služby IIS.  Skupiny jako prostředky společně na modul DSC, který slouží k uspořádání všechny požadované soubory v strukturu, která je přenosný a zahrnuje metadata k identifikaci, jak jsou prostředky určena k použití.

Následující témata popisují prostředky DSC:

- [Předdefinované prostředky DSC](builtInResource.md)
- [Sestavení vlastní prostředky DSC](authoringResource.md)
- [Předdefinované prostředky DSC pro Linux](lnxBuiltInResources.md)