---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 43b26426a76b6503a83e35ae0c02a0af69902ed6
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="declare-base-class"></a><span data-ttu-id="315a4-102">Deklarace základní třídy</span><span class="sxs-lookup"><span data-stu-id="315a4-102">Declare Base Class</span></span>
<span data-ttu-id="315a4-103">Třída prostředí Windows PowerShell je možné deklarovat jako základní typ pro jiné třídy prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="315a4-103">You can declare a Windows PowerShell class as a base type for another Windows PowerShell class.</span></span>

```powershell
class bar
{
   [int]foo()
       {
           return 100500
       }
}

class baz : bar {}

[baz]::new().foo() # return 100500
```

<span data-ttu-id="315a4-104">Existující typy rozhraní .NET Framework můžete také použít jako základní třídy:</span><span class="sxs-lookup"><span data-stu-id="315a4-104">You can also use existing .NET Framework types as base classes:</span></span>

```powershell
class MyIntList : system.collections.generic.list[int]
{

}

$list = [MyIntList]::new()

$list.Add(100)

$list[0] # return 100
```