---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 7ad4a00f7beba0de70696d88cd5448c7c638c50c
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/27/2017
---
# <a name="archive-cmdlets"></a>Rutiny archivu

Dvě nové rutiny, **Compress archivu** a **rozbalte archivu**, umožňují komprimovat a rozbalte soubory ZIP.

## <a name="compress-archive"></a>Komprimovat archivu
**Compress archivu** rutina vytvoří nový soubor archivu ze zadané soubory. Soubor archivu umožňuje soubory, které mají být zabalené a volitelně komprimované do jednoho souboru pro snadnější zpracování a úložiště. Pomocí zadané v algoritmus komprese lze komprimovat soubor archivu **- CompressionLevel** parametr.
```powershell
Compress-Archive -LiteralPath <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>] 
Compress-Archive [-Path] <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
```

## <a name="expand-archive"></a>Rozbalte archivu
**Rozbalte archivu** rutiny extrahuje soubory z archivu zadaný soubor. Soubor archivu umožňuje soubory, které mají být zabalené a volitelně komprimované do jednoho souboru pro snadnější zpracování a úložiště.
```powershell
Expand-Archive -LiteralPath <String> [-DestinationPath] <String>
Expand-Archive [-Path] <String> [-DestinationPath] <String>
```

