---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 116f79a95126d0a1c579a95ec99eb5d8b75cc1e0
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="declare-implemented-interface"></a>Deklarace implementovaného rozhraní

Je možné deklarovat implementovaných po základní typy nebo okamžitě po dvojtečkou (:), pokud neexistuje žádný základní typ zadaný. Všechny názvy typů oddělte čárkami. Je velmi podobné syntaxi C#.

```powershell
class MyComparable : system.IComparable
{
    [int] CompareTo([object] $obj)
    {
        return 0;
    }
}

class MyComparableBar : bar, system.IComparable
{
    [int] CompareTo([object] $obj)
    {
        return 0;
    }
}
```
