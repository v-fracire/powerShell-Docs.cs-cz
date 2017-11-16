---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Řazení objekty"
ms.assetid: 8530caa8-3ed4-4c56-aed7-1295dd9ba199
ms.openlocfilehash: 2df45c64656e74dc8b72957ce59f2a5e5ee663b6
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="sorting-objects"></a>Řazení objekty
Jsme můžete uspořádat zobrazených dat, aby bylo snazší ke kontrole pomocí **řazení objektu** rutiny. **Řazení objektu** přebírá název jeden nebo více vlastností seřadit a vrátí data o seřazené podle hodnoty těchto vlastností.

Vezměte v úvahu problém výpis Win32_SystemDriver instancí. Pokud chcete seřadit **stavu** a potom podle **název**, můžeme provést zadáním:

```
Get-WmiObject -Class Win32_SystemDriver | Sort-Object -Property State,Name | Format-Table -Property Name,State,Started,DisplayName -AutoSize -Wrap
```

Přestože je toto zdlouhavé zobrazení, můžete zobrazit položky s stejného stavu seskupeny dohromady:

```
Name           State   Started DisplayName
----           -----   ------- -----------
ACPI           Running    True Microsoft ACPI Driver
AFD            Running    True AFD
AmdK7          Running    True AMD K7 Processor Driver
AsyncMac       Running    True RAS Asynchronous Media Driver
...
Abiosdsk       Stopped   False Abiosdsk
ACPIEC         Stopped   False ACPIEC
aec            Stopped   False Microsoft Kernel Acoustic Echo Canceller
...
```

Můžete také řadit objekty v obráceném pořadí tak, že zadáte **sestupně** parametr. Obrátí pořadí řazení, aby názvy jsou seřazené ve vzestupném abecedním pořadí a čísla jsou seřazené podle sestupném velikost.

```
PS> Get-WmiObject -Class Win32_SystemDriver | Sort-Object -Property State,Name -Descending | Format-Table -Property Name,State,Started,DisplayName -AutoSize -Wrap

Name           State   Started DisplayName
----           -----   ------- -----------
WS2IFSL        Stopped   False Windows Socket 2.0 Non-IFS Service Provider Supp
                               ort Environment
wceusbsh       Stopped   False Windows CE USB Serial Host Driver...
...
wdmaud         Running    True Microsoft WINMM WDM Audio Compatibility Driver
Wanarp         Running    True Remote Access IP ARP Driver
...
```

