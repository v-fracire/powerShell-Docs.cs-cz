---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředky DSC"
ms.openlocfilehash: 62bf352b929d661e585e145e5aab0f44f13010a1
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-resources"></a>Prostředky DSC

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Požadované prostředky konfigurace stavu (DSC) poskytují stavební bloky pro konfiguraci DSC. Prostředek zpřístupní vlastnosti, které může být nakonfigurované (schéma) a obsahuje funkce skriptu prostředí PowerShell, které místní Configuration Manager (LCM) žádostí na "jej tak".

Prostředek může model něco jako obecný jako soubor nebo co nastavení serveru služby IIS.  Skupiny jako prostředky společně na modul DSC, který slouží k uspořádání všechny požadované soubory v strukturu, která je přenosný a zahrnuje metadata k identifikaci, jak jsou prostředky určena k použití.  

Následující témata popisují prostředky DSC:

- [Předdefinované prostředky DSC](builtInResource.md)
- [Sestavení vlastní prostředky DSC](authoringResource.md)
- [Předdefinované prostředky DSC pro Linux](lnxBuiltInResources.md)

