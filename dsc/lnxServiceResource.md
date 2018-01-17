---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "DSC pro Linux nxService prostředků"
ms.openlocfilehash: 4273ad59f15eedd08b07888ebb6ee51d039b72b3
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-for-linux-nxservice-resource"></a>DSC pro Linux nxService prostředků

**NxService** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě služeb v uzlu systému Linux.

## <a name="syntax"></a>Syntaxe

```
nxService <string> #ResourceName
{
    Name = <string>
    [ Controller = <string> { init | upstart | systemd }  ]
    [ Enabled = <bool> ]
    [ State = <string> { Running | Stopped } ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Properties
|  Vlastnost |  Popis | 
|---|---|
| Název| Název služby nebo démon ke konfiguraci.| 
| Řadiče| Typ řadiče služby použít při konfiguraci služby.| 
| Povoleno| Určuje, zda byla služba spuštěna při spuštění.| 
| Stav| Určuje, zda je služba spuštěná. Nastavením této vlastnosti "Stopped" zajistit, že služba není spuštěná. Nastavte ji na "Spuštěný" zajistit, že služba není spuštěná.| 
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.| 


## <a name="additional-information"></a>Další informace

**NxService** prostředků nebude vytvořit definici služby nebo skriptu pro službu, pokud neexistuje. Můžete použít prostředí PowerShell konfigurace požadovaného stavu **nxFile** prostředků prostředků ke správě existence nebo obsah souboru definice služby nebo skriptu.

## <a name="example"></a>Příklad

Následující příklad ukazuje konfiguraci služby "httpd" (pro serveru Apache HTTP Server), zaregistrována **SystemD** řadič služby.

```
Import-DSCResource -Module nx 

Node $node {
#Apache Service
nxService ApacheService 
{
Name = "httpd"
State = "running"
Enabled = $true
Controller = "systemd"
}
}
```

