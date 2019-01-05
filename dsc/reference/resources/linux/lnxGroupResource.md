---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxGroup
ms.openlocfilehash: c61b6ab4a8c56d085b5297dcfc7582187d54f946
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048198"
---
# <a name="dsc-for-linux-nxgroup-resource"></a>DSC pro Linux prostředek nxGroup

**NxGroup** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě místních skupin na uzlu systému Linux.

## <a name="syntax"></a>Syntaxe

```
nxGroup <string> #ResourceName
{
    GroupName = <string>
    [ Ensure = <string> { Absent | Present } ]
    [ Members = <string[]> ]
    [ MembersToInclude = <string[]> ]
    [ MembersToExclude = <string[]> ]
    [ DependsOn = <string[]> ]
}
```

## <a name="properties"></a>Properties

|  Vlastnost |  Popis |
|---|---|
| Název skupiny| Určuje název skupiny, pro které chcete zajistit určitý stav.|
| Zkontrolujte| Určuje, jestli se má zkontrolovat, zda skupina existuje. Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že tato skupina existuje. Nastavte ho na "Chybí" Ujistěte se, že že skupina neexistuje. Výchozí hodnota je "K dispozici".|
| Členové| Určuje členy, které tvoří skupinu.|
| MembersToInclude| Určuje, že budete muset zajistit, aby uživatelé jsou členy skupiny.|
| MembersToExclude| Určuje, že budete muset zajistit, aby uživatelé nejsou členy skupiny.|
| PreferredGroupID| Pokud je to možné nastaví id skupiny na zadanou hodnotu. Pokud id skupiny je aktuálně používán, použije se další id skupiny k dispozici.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = '[ResourceType]ResourceName'`.|

## <a name="example"></a>Příklad

Následující příklad zajistí, že uživatel monuser existuje a je členem skupiny "DBusers".

```powershell
Import-DSCResource -Module nx

Node $node {
    nxUser UserExample {
       UserName = 'monuser'
       Description = 'Monitoring user'
       Password = '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
       Ensure = 'Present'
       HomeDirectory = '/home/monuser'
    }

    nxGroup GroupExample {
       GroupName = 'DBusers'
       Ensure = 'Present'
       MembersToInclude = 'monuser'
       DependsOn = '[nxUser]UserExample'
    }
}
```