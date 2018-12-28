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
# <a name="selecting-parts-of-objects-select-object"></a><span data-ttu-id="16869-103">Výběr částí objektů (Select-Object)</span><span class="sxs-lookup"><span data-stu-id="16869-103">Selecting Parts of Objects (Select-Object)</span></span>

<span data-ttu-id="16869-104">Můžete použít **Select-Object** rutina pro vytvoření nových, vlastních objektů prostředí Windows PowerShell, které obsahují vlastnosti vybrali objekty, které slouží k jejich vytvoření.</span><span class="sxs-lookup"><span data-stu-id="16869-104">You can use the **Select-Object** cmdlet to create new, custom Windows PowerShell objects that contain properties selected from the objects you use to create them.</span></span> <span data-ttu-id="16869-105">Zadejte následující příkaz pro vytvoření nového objektu, který obsahuje pouze vlastnosti Name a FreeSpace třídy služby WMI Win32_LogicalDisk:</span><span class="sxs-lookup"><span data-stu-id="16869-105">Type the following command to create a new object that includes only the Name and FreeSpace properties of the Win32_LogicalDisk WMI class:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace

Name                                    FreeSpace
----                                    ---------
C:                                      50664845312
```

<span data-ttu-id="16869-106">Typ dat nejde zobrazit po vydání tohoto příkazu, ale pokud je výsledek, který má Get-Member kanálem po Select-Object, poznáte, že máte nový typ objektu, objekt PSCustomObject:</span><span class="sxs-lookup"><span data-stu-id="16869-106">You cannot see the type of data after issuing that command, but if you pipe the result to Get-Member after the Select-Object, you can tell that you have a new type of object, a PSCustomObject:</span></span>

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

<span data-ttu-id="16869-107">Select-Object má celou řadu uplatnění.</span><span class="sxs-lookup"><span data-stu-id="16869-107">Select-Object has many uses.</span></span> <span data-ttu-id="16869-108">Jeden z nich je replikace dat, který poté můžete upravit.</span><span class="sxs-lookup"><span data-stu-id="16869-108">One of them is replicating data that you can then modify.</span></span> <span data-ttu-id="16869-109">Teď zvládne problém, který jsme narazili v předchozí části.</span><span class="sxs-lookup"><span data-stu-id="16869-109">We can now handle the problem we ran across in the previous section.</span></span> <span data-ttu-id="16869-110">Abychom mohli aktualizovat hodnotu FreeSpace v našich nově vytvořené objekty a výstup bude obsahovat popisné označení:</span><span class="sxs-lookup"><span data-stu-id="16869-110">We can update the value of FreeSpace in our newly-created objects and the output will include the descriptive label:</span></span>

```
Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0; $_}
Name                                                                  FreeSpace
----                                                                  ---------
C:                                                                48317.7265625
```