---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Řazení objektů
ms.assetid: 8530caa8-3ed4-4c56-aed7-1295dd9ba199
ms.openlocfilehash: 272d550a67b206f9924ebe143eca2f5906c0a304
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30949974"
---
# <a name="sorting-objects"></a>Řazení objektů

Jsme můžete uspořádat zobrazených dat, aby bylo snazší ke kontrole pomocí **řazení objektu** rutiny. **Řazení objektu** přebírá název jeden nebo více vlastností seřadit a vrátí data o seřazené podle hodnoty těchto vlastností.

Vezměte v úvahu problém výpis Win32_SystemDriver instancí. Pokud chcete seřadit **stavu** a potom podle **název**, můžeme provést zadáním:

```powershell
Get-WmiObject -Class Win32_SystemDriver | Sort-Object -Property State,Name | Format-Table -Property Name,State,Started,DisplayName -AutoSize -Wrap
```

Přestože je toto zdlouhavé zobrazení, můžete zobrazit položky s stejného stavu seskupeny dohromady:

```output
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