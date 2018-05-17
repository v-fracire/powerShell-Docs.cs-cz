---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: d7aec1a2ba8964e877ddd7406609fe135b1eb462
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="call-base-class-method"></a>Volání metody základní třídy

Můžete přepsat existující metod v podtřídách. K tomuto účelu deklarace pomocí se stejným názvem a podpis metody:

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

Volání metody třídy base z přepsaného implementace, převést na základní třídu ($[baseclass –] to) u volání:

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

Všechny metody prostředí PowerShell jsou virtuální. Pomocí stejnou syntaxí, jako je tomu u přepsání můžete skrýt nevirtuálních metod rozhraní .NET v podtřídy: deklarujte pouze metody se stejným názvem a podpis.

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
