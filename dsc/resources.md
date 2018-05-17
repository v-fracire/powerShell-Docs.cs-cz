---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Prostředky DSC
ms.openlocfilehash: 27e16c39699bb96b2829744b5700f75f59f8802f
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="dsc-resources"></a>Prostředky DSC

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Požadované prostředky konfigurace stavu (DSC) poskytují stavební bloky pro konfiguraci DSC. Prostředek zpřístupní vlastnosti, které může být nakonfigurované (schéma) a obsahuje funkce skriptu prostředí PowerShell, které místní Configuration Manager (LCM) žádostí na "jej tak".

Prostředek může model něco jako obecný jako soubor nebo co nastavení serveru služby IIS.  Skupiny jako prostředky společně na modul DSC, který slouží k uspořádání všechny požadované soubory v strukturu, která je přenosný a zahrnuje metadata k identifikaci, jak jsou prostředky určena k použití.

Následující témata popisují prostředky DSC:

- [Předdefinované prostředky DSC](builtInResource.md)
- [Sestavení vlastní prostředky DSC](authoringResource.md)
- [Předdefinované prostředky DSC pro Linux](lnxBuiltInResources.md)