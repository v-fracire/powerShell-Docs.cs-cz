---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Opakováním úlohu pro objekt příkazu ForEach více objektů
ms.assetid: 6697a12d-2470-4ed6-b5bb-c35e5d525eb6
ms.openlocfilehash: 8b8002af3ade0905421760ce29cdc84b084236e9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="repeating-a-task-for-multiple-objects-foreach-object"></a><span data-ttu-id="b1727-103">Opakováním úlohu pro více objektů (ForEach-Object)</span><span class="sxs-lookup"><span data-stu-id="b1727-103">Repeating a Task for Multiple Objects (ForEach-Object)</span></span>

<span data-ttu-id="b1727-104">**ForEach-Object** rutiny pomocí blocích skriptu a popisovač $_ pro aktuální objekt kanálu umožňují spustit příkaz na každém objektu v kanálu.</span><span class="sxs-lookup"><span data-stu-id="b1727-104">The **ForEach-Object** cmdlet uses script blocks and the $_ descriptor for the current pipeline object to let you run a command on each object in the pipeline.</span></span> <span data-ttu-id="b1727-105">To lze provést některé složité úlohy.</span><span class="sxs-lookup"><span data-stu-id="b1727-105">This can be used to perform some complicated tasks.</span></span>

<span data-ttu-id="b1727-106">Jeden situaci, kdy to může být užitečné je manipulace s daty, aby byla užitečnější.</span><span class="sxs-lookup"><span data-stu-id="b1727-106">One situation where this can be useful is manipulating data to make it more useful.</span></span> <span data-ttu-id="b1727-107">Například třídy Win32_LogicalDisk z rozhraní WMI slouží k vrácení informací volného místa pro každý místní disk.</span><span class="sxs-lookup"><span data-stu-id="b1727-107">For example, the Win32_LogicalDisk class from WMI can be used to return free space information for each local disk.</span></span> <span data-ttu-id="b1727-108">Data jsou vrácena z hlediska bajtů, ale, takže je obtížné číst:</span><span class="sxs-lookup"><span data-stu-id="b1727-108">The data is returned in terms of bytes, however, which makes it difficult to read:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

<span data-ttu-id="b1727-109">Nemůžeme převést hodnotu FreeSpace na MB vydělením každé hodnoty ve 1024 dvakrát; Po první dělení dat je v kilobajtech a po druhé dělení je v megabajtech.</span><span class="sxs-lookup"><span data-stu-id="b1727-109">We can convert the FreeSpace value to megabytes by dividing each value by 1024 twice; after the first division, the data is in kilobytes, and after the second division it is megabytes.</span></span> <span data-ttu-id="b1727-110">Můžete to udělat v bloku skriptu ForEach-Object zadáním:</span><span class="sxs-lookup"><span data-stu-id="b1727-110">You can do that in a ForEach-Object script block by typing:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

<span data-ttu-id="b1727-111">Bohužel výstup se teď dat s žádné přidružené popiskem.</span><span class="sxs-lookup"><span data-stu-id="b1727-111">Unfortunately, the output is now data with no associated label.</span></span> <span data-ttu-id="b1727-112">Protože vlastnosti služby WMI, například to jsou jen pro čtení, nemůžete přímo převést FreeSpace.</span><span class="sxs-lookup"><span data-stu-id="b1727-112">Because WMI properties such as this are read-only, you cannot directly convert FreeSpace.</span></span> <span data-ttu-id="b1727-113">Pokud zadáte toto:</span><span class="sxs-lookup"><span data-stu-id="b1727-113">If you type this:</span></span>

```powershell
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

<span data-ttu-id="b1727-114">Zobrazí chybovou zprávu:</span><span class="sxs-lookup"><span data-stu-id="b1727-114">You get an error message:</span></span>

```output
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

<span data-ttu-id="b1727-115">Může měnit uspořádání dat pomocí některé pokročilé techniky, ale je jednodušší vytvořit nový objekt, a to pomocí **Select-Object**.</span><span class="sxs-lookup"><span data-stu-id="b1727-115">You could reorganize the data by using some advanced techniques, but a simpler approach is to create a new object, by using **Select-Object**.</span></span>