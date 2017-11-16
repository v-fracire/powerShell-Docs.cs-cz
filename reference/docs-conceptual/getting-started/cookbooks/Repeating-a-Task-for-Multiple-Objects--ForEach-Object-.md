---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Opakováním úlohu pro objekt příkazu ForEach více objektů"
ms.assetid: 6697a12d-2470-4ed6-b5bb-c35e5d525eb6
ms.openlocfilehash: 33ae2c76a512a651ba1b91d15d876608f0d43ccc
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="repeating-a-task-for-multiple-objects-foreach-object"></a>Opakováním úlohu pro více objektů (ForEach-Object)
**ForEach-Object** rutiny pomocí blocích skriptu a popisovač $_ pro aktuální objekt kanálu umožňují spustit příkaz na každém objektu v kanálu. To lze provést některé složité úlohy.

Jeden situaci, kdy to může být užitečné je manipulace s daty, aby byla užitečnější. Například třídy Win32_LogicalDisk z rozhraní WMI slouží k vrácení informací volného místa pro každý místní disk. Data jsou vrácena z hlediska bajtů, ale, takže je obtížné číst:

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

Nemůžeme převést hodnotu FreeSpace na MB vydělením každé hodnoty ve 1024 dvakrát; Po první dělení dat je v kilobajtech a po druhé dělení je v megabajtech. Můžete to udělat v bloku skriptu ForEach-Object zadáním:

```
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

Bohužel výstup se teď dat s žádné přidružené popiskem. Protože vlastnosti služby WMI, například to jsou jen pro čtení, nemůžete přímo převést FreeSpace. Pokud zadáte toto:

```
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Zobrazí chybovou zprávu:

```
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Může měnit uspořádání dat pomocí některé pokročilé techniky, ale je jednodušší vytvořit nový objekt, a to pomocí **Select-Object**.

