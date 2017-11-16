---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 1fd6d80d6b7effb4bd98c1594d64e531c4e5c9b5
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/27/2017
---
# <a name="call-base-class-constructor"></a><span data-ttu-id="0e1e8-102">Volat základní třída – konstruktor</span><span class="sxs-lookup"><span data-stu-id="0e1e8-102">Call Base Class Constructor</span></span>

<span data-ttu-id="0e1e8-103">Chcete-li zavolat podtřídy konstruktoru základní třídy, použijte klíčové slovo **základní**:</span><span class="sxs-lookup"><span data-stu-id="0e1e8-103">To call a base class constructor from a subclass, use the keyword **base**:</span></span>

```powershell
class A 
{
    [int]$a

    A([int]$a)
    {
        $this.a = $a
    }
}

class B : A
{
    B() : base(103) {}
}

[B]::new().a # return 103
```

<span data-ttu-id="0e1e8-104">Pokud základní třída má konstruktor výchozí (žádný parametr), můžete vynechat explicitní konstruktor volání:</span><span class="sxs-lookup"><span data-stu-id="0e1e8-104">If a base class has a default (no parameter) constructor, you can omit an explicit constructor call:</span></span>

```powershell
class C : B
{
    C([int]$c) {}
}
```

