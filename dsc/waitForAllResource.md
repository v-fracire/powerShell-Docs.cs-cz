---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "WaitForAll prostředek DSC"
ms.openlocfilehash: 2054d2af7cd7dd839c62e77c1d4b6eee5cff34ab
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-waitforall-resource"></a>WaitForAll prostředek DSC

> Platí pro: 5.0 a novější se prostředí Windows PowerShell

**WaitForAll** prostředků konfigurace požadovaného stavu (DSC) lze použít v rámci bloku uzlu v [konfigurace DSC](configurations.md) určete závislosti na konfiguraci na jiných uzlech.

Tento prostředek úspěšná, pokud Pokud prostředek určeného **ResourceName** vlastnost je v požadovaném stavu na všechny cílové uzly, které jsou definované v **NodeName** vlastnost.


## <a name="syntax"></a>Syntaxe

```
WaitForAll [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ RetryIntervalSec = [Uint64] ]
    [ RetryCount = [Uint32] ] 
    [ ThrottleLimit = [Uint32]]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   | 
|---|---| 
| resourceName| Název prostředku závislý na.| 
| NodeName| Cílové uzly závislý na prostředku.| 
| RetryIntervalSec| Počet sekund, než se budete pokoušet. Minimální hodnota je 1.| 
| retryCount| Maximální počet pokusů o opakování.| 
| ThrottleLimit| Počet počítačů pro připojení současně. Výchozí hodnota je výchozí pro nové cimsession.| 
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|


## <a name="example"></a>Příklad

Příklad toho, jak používat tento prostředek, naleznete v části [určení závislostí mezi uzly](crossNodeDependencies.md)

