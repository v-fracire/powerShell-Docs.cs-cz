---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Výběr části objektů, vyberte objekt
ms.assetid: 72e64b1a-d351-4500-9da3-24d8a71d7a92
ms.openlocfilehash: 323c57ba4462e20d9713fb74732989584f5a993f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953884"
---
# <a name="selecting-parts-of-objects-select-object"></a>Výběr částí objektů (Select-Object)

Můžete použít **Select-Object** rutiny k vytvoření nových, vlastních objektů prostředí Windows PowerShell, které obsahují vlastnosti vybrané objekty, které budete používat při jejich vytváření. Zadejte následující příkaz pro vytvoření nového objektu, který obsahuje pouze název a FreeSpace vlastnosti třídy Win32_LogicalDisk WMI:

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace

Name                                    FreeSpace
----                                    ---------
C:                                      50664845312
```

Po vydání tohoto příkazu nevidíte typu dat, ale pokud jste po Select-Object prostřednictvím kanálu výsledek, který má Get-člen, můžete zadat, že máte nový typ objektu, PSCustomObject:

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

Select-Object se mnoha způsoby. Jeden z nich se replikuje data, která pak můžete upravovat. Nyní jsme může zpracovávat problému, který jsme narazili v předchozí části. Aktualizujeme hodnotu FreeSpace v našem nově vytvořené objekty a výstup bude obsahovat popisné označení:

```
Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0; $_}
Name                                                                  FreeSpace
----                                                                  ---------
C:                                                                48317.7265625
```