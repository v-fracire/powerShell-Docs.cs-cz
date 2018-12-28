---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Výběr částí objektů vyberte objekt
ms.assetid: 72e64b1a-d351-4500-9da3-24d8a71d7a92
ms.openlocfilehash: 323c57ba4462e20d9713fb74732989584f5a993f
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404094"
---
# <a name="selecting-parts-of-objects-select-object"></a>Výběr částí objektů (Select-Object)

Můžete použít **Select-Object** rutina pro vytvoření nových, vlastních objektů prostředí Windows PowerShell, které obsahují vlastnosti vybrali objekty, které slouží k jejich vytvoření. Zadejte následující příkaz pro vytvoření nového objektu, který obsahuje pouze vlastnosti Name a FreeSpace třídy služby WMI Win32_LogicalDisk:

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace

Name                                    FreeSpace
----                                    ---------
C:                                      50664845312
```

Typ dat nejde zobrazit po vydání tohoto příkazu, ale pokud je výsledek, který má Get-Member kanálem po Select-Object, poznáte, že máte nový typ objektu, objekt PSCustomObject:

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace| Get-Member

   TypeName: System.Management.Automation.PSCustomObject

Name        MemberType   Definition
----        ----------   ----------
Equals      Method       System.Boolean Equals(Object obj)
GetHashCode Method       System.Int32 GetHashCode()
GetType     Method       System.Type GetType()
ToString    Method       System.String ToString()
FreeSpace   NoteProperty  FreeSpace=...
Name        NoteProperty System.String Name=C:
```

Select-Object má celou řadu uplatnění. Jeden z nich je replikace dat, který poté můžete upravit. Teď zvládne problém, který jsme narazili v předchozí části. Abychom mohli aktualizovat hodnotu FreeSpace v našich nově vytvořené objekty a výstup bude obsahovat popisné označení:

```
Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0; $_}
Name                                                                  FreeSpace
----                                                                  ---------
C:                                                                48317.7265625
```