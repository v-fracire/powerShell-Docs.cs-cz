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
# <a name="sorting-objects"></a><span data-ttu-id="e6e2d-103">Řazení objekty</span><span class="sxs-lookup"><span data-stu-id="e6e2d-103">Sorting Objects</span></span>
<span data-ttu-id="e6e2d-104">Jsme můžete uspořádat zobrazených dat, aby bylo snazší ke kontrole pomocí **řazení objektu** rutiny.</span><span class="sxs-lookup"><span data-stu-id="e6e2d-104">We can organize displayed data to make it easier to scan by using the **Sort-Object** cmdlet.</span></span> <span data-ttu-id="e6e2d-105">**Řazení objektu** přebírá název jeden nebo více vlastností seřadit a vrátí data o seřazené podle hodnoty těchto vlastností.</span><span class="sxs-lookup"><span data-stu-id="e6e2d-105">**Sort-Object** takes the name of one or more properties to sort on, and returns data sorted by the values of those properties.</span></span>

<span data-ttu-id="e6e2d-106">Vezměte v úvahu problém výpis Win32_SystemDriver instancí.</span><span class="sxs-lookup"><span data-stu-id="e6e2d-106">Consider the problem of listing Win32_SystemDriver instances.</span></span> <span data-ttu-id="e6e2d-107">Pokud chcete seřadit **stavu** a potom podle **název**, můžeme provést zadáním:</span><span class="sxs-lookup"><span data-stu-id="e6e2d-107">If we want to sort by **State** and then by **Name**, we can do it by typing:</span></span>

```
Get-WmiObject -Class Win32_SystemDriver | Sort-Object -Property State,Name | Format-Table -Property Name,State,Started,DisplayName -AutoSize -Wrap
```

<span data-ttu-id="e6e2d-108">Přestože je toto zdlouhavé zobrazení, můžete zobrazit položky s stejného stavu seskupeny dohromady:</span><span class="sxs-lookup"><span data-stu-id="e6e2d-108">Although this is a lengthy display, you can see items with the same state grouped together:</span></span>

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

<span data-ttu-id="e6e2d-109">Můžete také řadit objekty v obráceném pořadí tak, že zadáte **sestupně** parametr.</span><span class="sxs-lookup"><span data-stu-id="e6e2d-109">You can also sort the objects in reverse order by specifying the **Descending** parameter.</span></span> <span data-ttu-id="e6e2d-110">Obrátí pořadí řazení, aby názvy jsou seřazené ve vzestupném abecedním pořadí a čísla jsou seřazené podle sestupném velikost.</span><span class="sxs-lookup"><span data-stu-id="e6e2d-110">This reverses the sort order so that names are sorted in reverse alphabetical order and numbers are sorted by descending size.</span></span>

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

