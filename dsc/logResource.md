---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC Log
ms.openlocfilehash: 50fd6cd31ba426108830fcf124a767318060a95d
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268428"
---
# <a name="dsc-log-resource"></a>Prostředek DSC Log

_Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.0_

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
> Ve výchozím nastavení jsou povoleny pouze v provozních protokolech DSC. Předtím, než v analytickém protokolu bude k dispozici nebo viditelné, musí být povolena. Další informace najdete v tématu [kde jsou protokoly událostí DSC?](troubleshooting.md#where-are-dsc-event-logs).

## <a name="properties"></a>Properties

| Vlastnost | Popis |
| --- | --- |
| Zpráva| Určuje zprávu, kterou chcete zapisovat do protokolu událostí stavu Microsoft-Windows-Desired konfigurace/analýzy.|
| DependsOn | Označuje, že konfigurace jiný prostředek musí spustit před napsané tuto zprávu protokolu. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = '[ResourceType]ResourceName'`.|

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