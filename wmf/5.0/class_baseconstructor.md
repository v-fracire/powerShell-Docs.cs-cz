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
# <a name="call-base-class-constructor"></a>Volat základní třída – konstruktor

Chcete-li zavolat podtřídy konstruktoru základní třídy, použijte klíčové slovo **základní**:

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

Pokud základní třída má konstruktor výchozí (žádný parametr), můžete vynechat explicitní konstruktor volání:

```powershell
class C : B
{
    C([int]$c) {}
}
```

