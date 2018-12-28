---
ms.date: 08/25/2017
keywords: rutiny prostředí PowerShell
title: Objekt ObjectModelRoot
ms.openlocfilehash: 2670321ebac1eac4ecc8457afb796f9f260da471
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404106"
---
# <a name="the-objectmodelroot-object"></a>Objekt ObjectModelRoot

**$PsISE** instance třídy Microsoft.PowerShell.Host.ISE.ObjectModelRoot je objekt, který je hlavní kořenový objekt ve Windows Powershellu® integrovaném skriptovacím prostředí (ISE).
Toto téma popisuje vlastnosti **ObjectModelRoot** objektu.

## <a name="properties"></a>Properties

### <a name="currentfile"></a>CurrentFile

> Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, která načte soubor, který je spojen s tímto objektem hostitele, který má aktuálně fokus.

### <a name="currentpowershelltab"></a>CurrentPowerShellTab

> Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, který získává PowerShell tab, ke kterému má fokus.

### <a name="currentvisiblehorizontaltool"></a>CurrentVisibleHorizontalTool

> Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, který získá aktuálně viditelné nástroj Windows PowerShell ISE doplněk, který se nachází v podokně nástroj vodorovný v dolní části editoru.

### <a name="currentvisibleverticaltool"></a>CurrentVisibleVerticalTool

> Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, který získá aktuálně viditelné nástroj Windows PowerShell ISE doplněk, který se nachází v podokně svislý nástroj na pravé straně editoru.

### <a name="options"></a>Možnosti

> Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, který získá různé možnosti, které můžete změnit nastavení v prostředí Windows PowerShell ISE.

### <a name="powershelltabs"></a>PowerShellTabs

> Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, která získá kolekci karet prostředí PowerShell, které jsou otevřeny v prostředí Windows PowerShell ISE. Ve výchozím nastavení tento objekt obsahuje jedné karty Powershellu. Můžete však přidat další karty Powershellu k tomuto objektu, pomocí skriptů nebo použijte nabídky v prostředí Windows PowerShell ISE.

## <a name="see-also"></a>Viz také

- [Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)