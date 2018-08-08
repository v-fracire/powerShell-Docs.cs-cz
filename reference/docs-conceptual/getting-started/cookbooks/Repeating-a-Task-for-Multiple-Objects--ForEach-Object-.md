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
# <a name="repeating-a-task-for-multiple-objects-foreach-object"></a>Opakování úlohy s více objekty (ForEach-Object)

**ForEach-Object** rutina používá bloky skriptu a `$_` popisovač pro aktuální objekt kanálu pro umožňují spustit příkaz pro každý objekt v kanálu. To je možné provádět některé složité úkoly.

Jedna situace, kdy to může být užitečné je manipulace s daty, aby byla užitečnější. Například Třída Win32_LogicalDisk z rozhraní WMI lze použít k vrácení informací volného místa pro každý místní disk. Data jsou vrácena z hlediska bajtů, ale díky tomu mohou ztížit čtení:

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

Můžeme převést hodnotu FreeSpace megabajtů vydělí jednotlivé hodnoty 1024 dvakrát; Po první dělení dat je v kilobajtech a po druhé dělení je v megabajtech. Můžete to udělat v bloku skriptu ForEach-Object zadáním:

```
PS> Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

Bohužel výstupem jsou teď data žádné přidružené popiskem. Protože vlastnosti služby WMI, jako je to jsou jen pro čtení, nemůžete přímo převést FreeSpace. Pokud zadáte toto:

```powershell
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Zobrazí chybová zpráva:

```output
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Může měnit uspořádání dat s využitím některé pokročilé techniky, ale je jednodušší přístup k vytvoření nového objektu, pomocí **Select-Object**.