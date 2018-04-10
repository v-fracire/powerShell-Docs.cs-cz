---
ms.date: 08/25/2017
keywords: rutiny prostředí PowerShell
title: Objekt ObjectModelRoot
ms.openlocfilehash: 2670321ebac1eac4ecc8457afb796f9f260da471
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="the-objectmodelroot-object"></a>Objekt ObjectModelRoot

**$PsISE** objekt, který je hlavní kořenový objekt ve Windows PowerShell® Integrované skriptovací prostředí (ISE) je instance třídy Microsoft.PowerShell.Host.ISE.ObjectModelRoot.
Toto téma popisuje vlastnosti **ObjectModelRoot** objektu.

## <a name="properties"></a>Properties

### <a name="currentfile"></a>CurrentFile

> Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnost jen pro čtení, získá soubor, který je přidružen k tomuto objektu hostitele, který je aktuálně aktivní.

### <a name="currentpowershelltab"></a>CurrentPowerShellTab

> Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnost jen pro čtení, získá kartě prostředí PowerShell, který je aktivní.

### <a name="currentvisiblehorizontaltool"></a>CurrentVisibleHorizontalTool

> Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnost jen pro čtení, který získá aktuálně viditelné nástroj rozšíření Windows PowerShell ISE, který se nachází v podokně vodorovné nástrojů v dolní části editoru.

### <a name="currentvisibleverticaltool"></a>CurrentVisibleVerticalTool

> Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnost jen pro čtení, který získá aktuálně viditelné nástroj rozšíření Windows PowerShell ISE, který se nachází v podokně svislý nástroj na pravé straně editoru.

### <a name="options"></a>Možnosti

> Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnost jen pro čtení, který získá různé možnosti, které mohou změnit nastavení v systému Windows PowerShell ISE.

### <a name="powershelltabs"></a>PowerShellTabs

> Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnost jen pro čtení, získá kolekci karet prostředí PowerShell, které jsou otevřeny v systému Windows PowerShell ISE. Ve výchozím nastavení tento objekt obsahuje jedné karty prostředí PowerShell. Můžete ale přidat další karty prostředí PowerShell k tomuto objektu, pomocí skriptů nebo pomocí nabídek v systému Windows PowerShell ISE.

## <a name="see-also"></a>Viz také

- [Účelem ISE Windows PowerShell skriptování objektový Model](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)