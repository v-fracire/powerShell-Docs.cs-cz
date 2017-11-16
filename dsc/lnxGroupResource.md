---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "DSC pro Linux nxGroup prostředků"
ms.openlocfilehash: fcd1dfd3110b1358ed7ef9ca8d57154186b271f6
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-for-linux-nxgroup-resource"></a>DSC pro Linux nxGroup prostředků

**NxGroup** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě místních skupin na uzlu Linux.

## <a name="syntax"></a>Syntaxe

```powershell
nxGroup <string> #ResourceName
{
    GroupName = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Members = <string[]> ]
    [ MebersToInclude = <string[]>]
    [ MembersToExclude = <string[]> ]
    [ DependsOn = <string[]> ]
}

```

## <a name="properties"></a>Properties

|  Vlastnost |  Popis | 
|---|---|
| Název skupiny| Určuje název skupiny, pro které chcete zajistit určitý stav.| 
| Ujistěte se| Určuje, jestli se má zkontrolovat, zda skupina existuje. Nastavením této vlastnosti "Přítomen" Ujistěte se, že existuje daná skupina. Nastavte ji na "Chybí" Ujistěte se, že že skupina neexistuje. Výchozí hodnota je "Dispozici".| 
| Členové| Určuje členů, které tvoří skupinu.| 
| MembersToInclude| Určuje, že uživatelé, kteří chcete zajistit jsou členy skupiny.| 
| MembersToExclude| Určuje, že uživatelé, kteří chcete zajistit nejsou členy skupiny.| 
| PreferredGroupID| Pokud je to možné nastaví na zadanou hodnotu id skupiny. Pokud id skupiny je aktuálně používán, použije se další id skupiny k dispozici.| 
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.| 

## <a name="example"></a>Příklad

Následující příklad zajistí, že uživatel "monuser" existuje a je členem skupiny "DBusers".

```
Import-DSCResource -Module nx 

Node $node {

nxUser UserExample{
   UserName = "monuser"
   Description = "Monitoring user"
   Password  =    '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
   Ensure = "Present"
   HomeDirectory = "/home/monuser"
}
 
nxGroup GroupExample{
   GroupName = "DBusers"
   Ensure = "Present"
   MembersToInclude = "monuser"
   DependsOn = "[nxUser]UserExample"            
}
}
```

