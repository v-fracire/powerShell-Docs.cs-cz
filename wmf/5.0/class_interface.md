---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 116f79a95126d0a1c579a95ec99eb5d8b75cc1e0
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34225483"
---
# <a name="declare-implemented-interface"></a><span data-ttu-id="0dacc-102">Deklarace implementovaného rozhraní</span><span class="sxs-lookup"><span data-stu-id="0dacc-102">Declare Implemented Interface</span></span>

<span data-ttu-id="0dacc-103">Je možné deklarovat implementovaných po základní typy nebo okamžitě po dvojtečkou (:), pokud neexistuje žádný základní typ zadaný.</span><span class="sxs-lookup"><span data-stu-id="0dacc-103">You can declare implemented interfaces after base types, or immediately after a colon (:), if there is no base type specified.</span></span> <span data-ttu-id="0dacc-104">Všechny názvy typů oddělte čárkami.</span><span class="sxs-lookup"><span data-stu-id="0dacc-104">Separate all type names by using commas.</span></span> <span data-ttu-id="0dacc-105">Je velmi podobné syntaxi C#.</span><span class="sxs-lookup"><span data-stu-id="0dacc-105">It’s very similar to C# syntax.</span></span>

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
