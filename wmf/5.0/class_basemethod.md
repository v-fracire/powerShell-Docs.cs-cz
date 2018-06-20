---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: d7aec1a2ba8964e877ddd7406609fe135b1eb462
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219738"
---
# <a name="call-base-class-method"></a><span data-ttu-id="40d29-102">Volání metody základní třídy</span><span class="sxs-lookup"><span data-stu-id="40d29-102">Call Base Class Method</span></span>

<span data-ttu-id="40d29-103">Můžete přepsat existující metod v podtřídách.</span><span class="sxs-lookup"><span data-stu-id="40d29-103">You can override existing methods in subclasses.</span></span> <span data-ttu-id="40d29-104">K tomuto účelu deklarace pomocí se stejným názvem a podpis metody:</span><span class="sxs-lookup"><span data-stu-id="40d29-104">To do this, declare methods by using the same name and signature:</span></span>

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

<span data-ttu-id="40d29-105">Volání metody třídy base z přepsaného implementace, převést na základní třídu ($[baseclass –] to) u volání:</span><span class="sxs-lookup"><span data-stu-id="40d29-105">To call base class methods from overridden implementations, cast to the base class ([baseClass]$this) on invocation:</span></span>

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

<span data-ttu-id="40d29-106">Všechny metody prostředí PowerShell jsou virtuální.</span><span class="sxs-lookup"><span data-stu-id="40d29-106">All PowerShell methods are virtual.</span></span> <span data-ttu-id="40d29-107">Pomocí stejnou syntaxí, jako je tomu u přepsání můžete skrýt nevirtuálních metod rozhraní .NET v podtřídy: deklarujte pouze metody se stejným názvem a podpis.</span><span class="sxs-lookup"><span data-stu-id="40d29-107">You can hide non-virtual .NET methods in a subclass by using the same syntax as you do for an override: just declare methods with same name and signature.</span></span>

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
