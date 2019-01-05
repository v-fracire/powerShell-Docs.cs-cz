---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxService
ms.openlocfilehash: fe8043995205649378725f2ab0a78e19313739c9
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048119"
---
# <a name="dsc-for-linux-nxservice-resource"></a>DSC pro Linux prostředek nxService

**NxService** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě služeb na uzlech systému Linux.

## <a name="syntax"></a>Syntaxe

```
nxService <string> #ResourceName
{
    Name = <string>
    [ Controller = <string> { init | upstart | systemd } ]
    [ Enabled = <bool> ]
    [ State = <string> { Running | Stopped } ]
    [ DependsOn = <string[]> ]
}
```

## <a name="properties"></a>Properties

| Vlastnost | Popis |
|---|---|
| Name| Název služby/démona ke konfiguraci.|
| Kontroler| Typ služby řadiče pro použití při konfiguraci služby.|
| Enabled| Určuje, zda bude služba spuštěna při spuštění.|
| Stav| Určuje, zda je služba spuštěna. Nastavte tuto vlastnost na "Stopped" Ujistěte se, že služba není spuštěná. Nastavte na "Spuštěno" Ujistěte se, že služba není spuštěná.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="additional-information"></a>Další informace

**NxService** prostředek nebude vytvořit definice nebo skript pro službu, pokud neexistuje. Můžete použít PowerShell Desired State Configuration **nxFile** prostředky ke správě existenci nebo obsah definičního souboru služby nebo skriptu.

## <a name="example"></a>Příklad

Následující příklad ukazuje konfiguraci služby "httpd" (v případě serveru Apache HTTP Server), zaregistrované **SystemD** řadič služby.

```powershell
Import-DSCResource -Module nx

Node $node {
    #Apache Service
    nxService ApacheService {
        Name = 'httpd'
        State = 'running'
        Enabled = $true
        Controller = 'systemd'
    }
}
```