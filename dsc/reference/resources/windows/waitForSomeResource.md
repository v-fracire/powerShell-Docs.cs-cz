---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: WaitForSome prostředků DSC
ms.openlocfilehash: 906375a8fcf9b87d4b7487e63e6fae3f05b86d0d
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048117"
---
# <a name="dsc-waitforsome-resource"></a>WaitForSome prostředků DSC

> Platí pro: Prostředí Windows PowerShell 5.0 a novější

**WaitForAny** Desired State Configuration (DSC) prostředku se dá použít v bloku uzlu v [konfigurace DSC](../../../configurations/configurations.md) postup určení závislostí pro konfigurací na jiných uzlech.

Tento prostředek proběhne úspěšně, pokud zadaný prostředek podle **ResourceName** vlastnost je v požadovaném stavu na minimální počet uzlů (určená **NodeCount**) definované **NodeName**  vlastnost.


## <a name="syntax"></a>Syntaxe

```
WaitForSome [String] #ResourceName
{
    NodeCount = [UInt32]
    NodeName = [string[]]
    ResourceName = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
    [RetryCount = [UInt32]]
    [RetryIntervalSec = [UInt64]]
    [ThrottleLimit = [UInt32]]
}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| NodeCount| Minimální počet uzlů, které musí být v požadovaném stavu pro tento prostředek proběhla úspěšně.|
| NodeName| Cílové uzly jsou závislé na prostředku.|
| ResourceName| Název prostředku, aby závisely na. Pokud tento prostředek patří do jiné konfigurace, formátování názvu jako "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "|
| RetryIntervalSec| Počet sekund, než to zkusíte znovu. Minimální hodnota je 1.|
| retryCount| Maximální počet pokusů o zopakování.|
| ThrottleLimit| Počet počítačů současně připojit. Výchozí hodnota je nový cimsession výchozí.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|
| PsDscRunAsCredential | Zobrazit [DSC pomocí uživatelských přihlašovacích údajů](https://docs.microsoft.com/powershell/dsc/runasuser) |

## <a name="example"></a>Příklad

Příklad toho, jak používat tento prostředek, naleznete v tématu [určení závislostí mezi uzly](../../../configurations/crossNodeDependencies.md)
