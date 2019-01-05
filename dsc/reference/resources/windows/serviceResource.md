---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC služby
ms.openlocfilehash: 09571bd0eaa428e7d0bb7a533d6ad1c0c936e2cf
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048115"
---
# <a name="dsc-service-resource"></a>Prostředek DSC služby

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0


**Služby** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě služeb na cílový uzel.

## <a name="syntax"></a>Syntaxe

```
Service [string] #ResourceName
{
    Name = [string]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Description = [string] ]
    [ DisplayName = [string] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Path = [string] ]
}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| Name| Určuje název služby. Všimněte si, že někdy se liší od zobrazovaný název. Můžete získat seznam služeb a jejich aktuální stav pomocí rutiny Get-Service.|
| BuiltInAccount| Určuje přihlašovací účet, který chcete použít pro službu. Hodnoty, které jsou pro tuto vlastnost povolena jsou: **LocalService**, **LocalSystem**, a **NetworkService**.|
| Přihlašovací údaje| Určuje přihlašovací údaje pro účet, který bude tato služba spuštěna pod. Tato vlastnost a __BuiltinAccount__ vlastnost nelze použít společně.|
| DependsOn| Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|
| Typ spuštění| Určuje typ spouštění služby. Hodnoty, které jsou pro tuto vlastnost povolena jsou: **Automatické**, **zakázané**, a **ruční**|
| Stav| Označuje stavu, ve kterém chcete zajistit pro službu.|
| Popis | Určuje popis cílové služby.|
| DisplayName | Určuje zobrazovaný název cílové služby.|
| Zkontrolujte | Určuje, zda cílová služba existuje v systému. Tuto vlastnost nastavte na **chybí** zajistit, že cílová služba neexistuje. Nastavení na **k dispozici** (výchozí hodnota) zajišťuje, že cílová služba existuje.|
| Cesta | Určuje cestu k binárnímu souboru pro novou službu.|

## <a name="example"></a>Příklad

```powershell
configuration ServiceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        Service ServiceExample
        {
            Name        = "TermService"
            StartupType = "Manual"
            State       = "Running"
        }
    }
}
```