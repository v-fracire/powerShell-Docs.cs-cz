---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 5dbaa126cf9ae3917c3a8787ffc5ef5ac77b19c1
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/27/2017
---
# <a name="declare-base-class"></a><span data-ttu-id="d63ad-102">Základní třídu deklarovat</span><span class="sxs-lookup"><span data-stu-id="d63ad-102">Declare Base Class</span></span>
<span data-ttu-id="d63ad-103">Třída prostředí Windows PowerShell je možné deklarovat jako základní typ pro jiné třídy prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d63ad-103">You can declare a Windows PowerShell class as a base type for another Windows PowerShell class.</span></span>

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

<span data-ttu-id="d63ad-104">Existující typy rozhraní .NET Framework můžete také použít jako základní třídy:</span><span class="sxs-lookup"><span data-stu-id="d63ad-104">You can also use existing .NET Framework types as base classes:</span></span>

```powershell
class MyIntList : system.collections.generic.list[int]
{
    
}

$list = [MyIntList]::new()

$list.Add(100)

$list[0] # return 100
```

