---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC Log
ms.openlocfilehash: 1f94a2d847a4ef63f81e2fb83d1a0f76f5677b09
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048140"
---
# <a name="dsc-log-resource"></a>Prostředek DSC Log

> _Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0_

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
> Ve výchozím nastavení jsou povoleny pouze v provozních protokolech DSC. Předtím, než v analytickém protokolu bude k dispozici nebo viditelné, musí být povolena. Další informace najdete v tématu [kde jsou protokoly událostí DSC?](../../../troubleshooting/troubleshooting.md#where-are-dsc-event-logs).

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
