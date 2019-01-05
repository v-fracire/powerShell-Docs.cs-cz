---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: WaitForAny prostředků DSC
ms.openlocfilehash: 39e90f0df3459b8891ed46e02ae82c45a285e7f5
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048143"
---
# <a name="dsc-waitforany-resource"></a>WaitForAny prostředků DSC

> Platí pro: Prostředí Windows PowerShell 5.1 a novější

**WaitForSome** Desired State Configuration (DSC) prostředku se dá použít v bloku uzlu v [konfigurace DSC](../../../configurations/configurations.md) postup určení závislostí pro konfigurací na jiných uzlech.

Tento prostředek proběhne úspěšně, pokud zadaný prostředek podle **ResourceName** vlastnost je v požadovaném stavu na všechny cílové uzly podle **NodeName** vlastnost.


## <a name="syntax"></a>Syntaxe

```
WaitForAny [string] #ResourceName
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

Příklad toho, jak používat tento prostředek, naleznete v tématu [určení závislostí mezi uzly](../../../configurations/crossNodeDependencies.md)
