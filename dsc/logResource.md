---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC Log
ms.openlocfilehash: fade94efd8133ae0172737e4bb1aed89fc0f97d9
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093472"
---
# <a name="dsc-log-resource"></a>Prostředek DSC Log

> Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

__Protokolu__ prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro zápis zpráv do protokolu událostí Microsoft-Windows-Desired State Configuration / analýzy.

```
Syntax

Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
}
```

> [!NOTE]
> Ve výchozím nastavení jsou povoleny pouze v provozních protokolech DSC. Předtím, než v analytickém protokolu bude k dispozici nebo viditelné, musí být povolena. Další informace najdete v tématu [kde jsou protokoly událostí DSC?](https://msdn.microsoft.com/en-us/powershell/dsc/troubleshooting#where-are-dsc-event-logs).

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| Zpráva| Určuje zprávu, kterou chcete zapisovat do protokolu událostí stavu Microsoft-Windows-Desired konfigurace/analýzy.|
| DependsOn | Označuje, že konfigurace jiný prostředek musí spustit před napsané tuto zprávu protokolu. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = '[ResourceType]ResourceName'`.|

## <a name="example"></a>Příklad

Následující příklad ukazuje, jak zahrnout zprávy v protokolu událostí stavu Microsoft-Windows-Desired konfigurace/analýzy.

> [!NOTE]
> Pokud spustíte [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) se tento prostředek nakonfigurován, bude vždy vrátí **$false**.

```powershell
Configuration logResourceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node localhost
    {
        Log LogExample
        {
            Message = 'This message will appear in the Microsoft-Windows-Desired State Configuration/Analytic event log.'
        }
    }
}
```