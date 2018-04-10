---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Prostředek DSC protokolu
ms.openlocfilehash: f1a528767508d4a0e7f0ea2e58fd27a6a4d7ec75
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-log-resource"></a>Prostředek DSC protokolu

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

__Protokolu__ prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro zápis zpráv do protokolu událostí stavu Microsoft-Windows-požadovaná konfigurace nebo analýzu.

```
Syntax

Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
}
```

Poznámka: Ve výchozím nastavení pouze v provozních protokolech DSC jsou povolené.
Před analytické protokolu bude k dispozici nebo viditelná, musí být povolena.
Najdete v následujícím článku.

[Kde jsou protokoly událostí DSC?](https://msdn.microsoft.com/en-us/powershell/dsc/troubleshooting#where-are-dsc-event-logs)

## <a name="properties"></a>Properties
|  Vlastnost  |  Popis   |
|---|---|
| Zpráva| Určuje zprávu, kterou chcete zapisovat do protokolu událostí Microsoft-Windows-Desired stav konfigurace nebo analýzu.|
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než získá zapsat tuto zprávu protokolu. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Příklad

Následující příklad ukazuje, jak chcete zahrnout zprávy v protokolu událostí Microsoft-Windows-Desired stav konfigurace nebo analýzu.

> **Poznámka:**: Pokud spustíte [Test DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) se tento prostředek nakonfigurován, bude vždy vrátí **$false**.

```powershell
Configuration logResourceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node localhost

    {
        Log LogExample
        {
            Message = "This message will appear in the Microsoft-Windows-Desired State Configuration/Analytic event log."
        }
    }
}
```