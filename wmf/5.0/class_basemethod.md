---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: eeafdd8d7a50e0bfc5ebd0ca8e9852c3d7405bf0
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="call-base-class-method"></a><span data-ttu-id="c02c6-102">Volání metody základní třídy</span><span class="sxs-lookup"><span data-stu-id="c02c6-102">Call Base Class Method</span></span>

<span data-ttu-id="c02c6-103">Můžete přepsat existující metod v podtřídách.</span><span class="sxs-lookup"><span data-stu-id="c02c6-103">You can override existing methods in subclasses.</span></span> <span data-ttu-id="c02c6-104">K tomuto účelu deklarace pomocí se stejným názvem a podpis metody:</span><span class="sxs-lookup"><span data-stu-id="c02c6-104">To do this, declare methods by using the same name and signature:</span></span>

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

<span data-ttu-id="c02c6-105">Volání metody třídy base z přepsaného implementace, převést na základní třídu ($[baseclass –] to) u volání:</span><span class="sxs-lookup"><span data-stu-id="c02c6-105">To call base class methods from overridden implementations, cast to the base class ([baseClass]$this) on invocation:</span></span>

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

<span data-ttu-id="c02c6-106">Všechny metody prostředí PowerShell jsou virtuální.</span><span class="sxs-lookup"><span data-stu-id="c02c6-106">All PowerShell methods are virtual.</span></span> <span data-ttu-id="c02c6-107">Pomocí stejnou syntaxí, jako je tomu u přepsání můžete skrýt nevirtuálních metod rozhraní .NET v podtřídy: deklarujte pouze metody se stejným názvem a podpis.</span><span class="sxs-lookup"><span data-stu-id="c02c6-107">You can hide non-virtual .NET methods in a subclass by using the same syntax as you do for an override: just declare methods with same name and signature.</span></span>

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