---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 0c450d765531c18c0b73c5c64262e9895f92068a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="archive-cmdlets"></a>Rutiny archivu

Dvě nové rutiny, **Compress archivu** a **rozbalte archivu**, umožňují komprimovat a rozbalte soubory ZIP.

## <a name="compress-archive"></a>Compress-Archive
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