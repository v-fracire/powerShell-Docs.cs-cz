---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 7817769c3fc060a51c833b7469f7b556b9b40e87
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/27/2017
---
# <a name="call-base-class-method"></a><span data-ttu-id="e5a7d-102">Volání metody třídy Base</span><span class="sxs-lookup"><span data-stu-id="e5a7d-102">Call Base Class Method</span></span>

<span data-ttu-id="e5a7d-103">Můžete přepsat existující metod v podtřídách.</span><span class="sxs-lookup"><span data-stu-id="e5a7d-103">You can override existing methods in subclasses.</span></span> <span data-ttu-id="e5a7d-104">K tomuto účelu deklarace pomocí se stejným názvem a podpis metody:</span><span class="sxs-lookup"><span data-stu-id="e5a7d-104">To do this, declare methods by using the same name and signature:</span></span>

```powershell
class baseClass
{
    [int]foo() {return 100500}
}

class childClass1 : baseClass
{
    [int]foo() {return 200600}
}

[childClass1]::new().foo() # return 200600
```

<span data-ttu-id="e5a7d-105">Volání metody třídy base z přepsaného implementace, převést na základní třídu ($[baseclass –] to) u volání:</span><span class="sxs-lookup"><span data-stu-id="e5a7d-105">To call base class methods from overridden implementations, cast to the base class ([baseClass]$this) on invocation:</span></span>

```powershell
class childClass2 : baseClass
{
    [int]foo()
    {
        return 3 * ([baseClass]$this).foo()
    }
}

[childClass2]::new().foo() # return 301500
```

<span data-ttu-id="e5a7d-106">Všechny metody prostředí PowerShell jsou virtuální.</span><span class="sxs-lookup"><span data-stu-id="e5a7d-106">All PowerShell methods are virtual.</span></span> <span data-ttu-id="e5a7d-107">Pomocí stejnou syntaxí, jako je tomu u přepsání můžete skrýt nevirtuálních metod rozhraní .NET v podtřídy: deklarujte pouze metody se stejným názvem a podpis.</span><span class="sxs-lookup"><span data-stu-id="e5a7d-107">You can hide non-virtual .NET methods in a subclass by using the same syntax as you do for an override: just declare methods with same name and signature.</span></span>

```powershell
class MyIntList : system.collections.generic.list[int]
{
    # Add is final in system.collections.generic.list
    [void] Add([int]$arg)
    {
        ([system.collections.generic.list[int]]$this).Add($arg * 2)
    }
}

$list = [MyIntList]::new()
$list.Add(100)
$list[0] # return 200
```

