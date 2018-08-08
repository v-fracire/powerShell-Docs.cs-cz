---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Opakování úlohy s více objekty ForEach objektu
ms.assetid: 6697a12d-2470-4ed6-b5bb-c35e5d525eb6
ms.openlocfilehash: 64d85edad4a6931b2376b95b6d1f5b4d5194399f
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587257"
---
# <a name="repeating-a-task-for-multiple-objects-foreach-object"></a><span data-ttu-id="b8bcf-103">Opakování úlohy s více objekty (ForEach-Object)</span><span class="sxs-lookup"><span data-stu-id="b8bcf-103">Repeating a Task for Multiple Objects (ForEach-Object)</span></span>

<span data-ttu-id="b8bcf-104">**ForEach-Object** rutina používá bloky skriptu a `$_` popisovač pro aktuální objekt kanálu pro umožňují spustit příkaz pro každý objekt v kanálu.</span><span class="sxs-lookup"><span data-stu-id="b8bcf-104">The **ForEach-Object** cmdlet uses script blocks and the `$_` descriptor for the current pipeline object to let you run a command on each object in the pipeline.</span></span> <span data-ttu-id="b8bcf-105">To je možné provádět některé složité úkoly.</span><span class="sxs-lookup"><span data-stu-id="b8bcf-105">This can be used to perform some complicated tasks.</span></span>

<span data-ttu-id="b8bcf-106">Jedna situace, kdy to může být užitečné je manipulace s daty, aby byla užitečnější.</span><span class="sxs-lookup"><span data-stu-id="b8bcf-106">One situation where this can be useful is manipulating data to make it more useful.</span></span> <span data-ttu-id="b8bcf-107">Například Třída Win32_LogicalDisk z rozhraní WMI lze použít k vrácení informací volného místa pro každý místní disk.</span><span class="sxs-lookup"><span data-stu-id="b8bcf-107">For example, the Win32_LogicalDisk class from WMI can be used to return free space information for each local disk.</span></span> <span data-ttu-id="b8bcf-108">Data jsou vrácena z hlediska bajtů, ale díky tomu mohou ztížit čtení:</span><span class="sxs-lookup"><span data-stu-id="b8bcf-108">The data is returned in terms of bytes, however, which makes it difficult to read:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

<span data-ttu-id="b8bcf-109">Můžeme převést hodnotu FreeSpace megabajtů vydělí jednotlivé hodnoty 1024 dvakrát; Po první dělení dat je v kilobajtech a po druhé dělení je v megabajtech.</span><span class="sxs-lookup"><span data-stu-id="b8bcf-109">We can convert the FreeSpace value to megabytes by dividing each value by 1024 twice; after the first division, the data is in kilobytes, and after the second division it is megabytes.</span></span> <span data-ttu-id="b8bcf-110">Můžete to udělat v bloku skriptu ForEach-Object zadáním:</span><span class="sxs-lookup"><span data-stu-id="b8bcf-110">You can do that in a ForEach-Object script block by typing:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

<span data-ttu-id="b8bcf-111">Bohužel výstupem jsou teď data žádné přidružené popiskem.</span><span class="sxs-lookup"><span data-stu-id="b8bcf-111">Unfortunately, the output is now data with no associated label.</span></span> <span data-ttu-id="b8bcf-112">Protože vlastnosti služby WMI, jako je to jsou jen pro čtení, nemůžete přímo převést FreeSpace.</span><span class="sxs-lookup"><span data-stu-id="b8bcf-112">Because WMI properties such as this are read-only, you cannot directly convert FreeSpace.</span></span> <span data-ttu-id="b8bcf-113">Pokud zadáte toto:</span><span class="sxs-lookup"><span data-stu-id="b8bcf-113">If you type this:</span></span>

```powershell
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

<span data-ttu-id="b8bcf-114">Zobrazí chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="b8bcf-114">You get an error message:</span></span>

```output
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

<span data-ttu-id="b8bcf-115">Může měnit uspořádání dat s využitím některé pokročilé techniky, ale je jednodušší přístup k vytvoření nového objektu, pomocí **Select-Object**.</span><span class="sxs-lookup"><span data-stu-id="b8bcf-115">You could reorganize the data by using some advanced techniques, but a simpler approach is to create a new object, by using **Select-Object**.</span></span>