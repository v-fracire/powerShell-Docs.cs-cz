---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: WaitForAll prostředků DSC
ms.openlocfilehash: 367f95caaa71ebec9c8e0a7c31fa5c0f5be27945
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2018
ms.locfileid: "50226096"
---
# <a name="dsc-waitforall-resource"></a>WaitForAll prostředků DSC

> Platí pro: 5.0 a novější se prostředí Windows PowerShell

**WaitForAll** Desired State Configuration (DSC) prostředku se dá použít v bloku uzlu v [konfigurace DSC](configurations.md) postup určení závislostí pro konfigurací na jiných uzlech.

Tento prostředek proběhne úspěšně, pokud zadaný prostředek podle **ResourceName** vlastnost je v požadovaném stavu na všechny cílové uzly podle **NodeName** vlastnost.


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
| ResourceName| Název prostředku, aby závisely na. Pokud tento prostředek patří do jiné konfigurace, formátování názvu jako "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "|
| NodeName| Cílové uzly jsou závislé na prostředku.|
| RetryIntervalSec| Počet sekund, než to zkusíte znovu. Minimální hodnota je 1.|
| retryCount| Maximální počet pokusů o zopakování.|
| ThrottleLimit| Počet počítačů současně připojit. Výchozí hodnota je nový cimsession výchozí.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|


## <a name="example"></a>Příklad

Příklad toho, jak používat tento prostředek, naleznete v tématu [určení závislostí mezi uzly](crossNodeDependencies.md)