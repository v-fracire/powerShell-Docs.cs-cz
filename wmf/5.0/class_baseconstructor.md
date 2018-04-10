---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 3269c8cc871f22488b64fb072dac72698983f360
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="call-base-class-constructor"></a>Volání konstruktoru základní třídy

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