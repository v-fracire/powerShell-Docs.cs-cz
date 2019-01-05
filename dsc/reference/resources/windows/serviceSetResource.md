---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek Serviceset DSC
ms.openlocfilehash: 5694c2abc5c0caf0098670b629af464b35125583
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048120"
---
# <a name="dsc-serviceset-resource"></a>Prostředek Serviceset DSC

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

**ServiceSet** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě služeb na cílový uzel. Tento prostředek je [složený prostředek](../../../resources/authoringResourceComposite.md) , která volá [služeb resource](serviceResource.md) pro každou službu podle `Name` vlastnost.

Pokud chcete provést konfiguraci celé řady služeb do stejného stavu, použijte tento prostředek.

## <a name="syntax"></a>Syntaxe

```
Service [string] #ResourceName
{
    Name = [string[]]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Ensure = [string] { Absent | Present }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| Name| Určuje názvy služeb. Všimněte si, že někdy se liší od zobrazované názvy. Můžete získat seznam služeb a jejich aktuální stav s [Get-Service](https://technet.microsoft.com/library/hh849804.aspx) rutiny.|
| Typ spuštění| Určuje typ spouštění služby. Hodnoty, které jsou pro tuto vlastnost povolena jsou: **Automatické**, **zakázané**, a **ruční**|
| BuiltInAccount| Určuje přihlašovací účet, který chcete použít pro služby. Hodnoty, které jsou pro tuto vlastnost povolena jsou: **LocalService**, **LocalSystem**, a **NetworkService**.|
| Stav| Označuje stavu, ve kterém chcete zajistit služby: **Zastavit** nebo **systémem**.|
| Zkontrolujte| Určuje, zda služby existovat v systému. Tuto vlastnost nastavte na **chybí** zajistit, že služby neexistuje. Nastavení na **k dispozici** (výchozí hodnota) zajišťuje, že existují cílové služby.|
| Přihlašovací údaje| Určuje přihlašovací údaje pro účet, pod kterými poběží prostředek služby. Tato vlastnost a **BuiltinAccount** vlastnost nelze použít společně.|
| DependsOn| Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba *ResourceName* a jejím typem je *ResourceType*, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|



## <a name="example"></a>Příklad

Následující konfigurace spuštění služby "Windows zvuku" a "Služby Vzdálená plocha".

```powershell
configuration ServiceSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        ServiceSet ServiceSetExample
        {
            Name        = @("TermService", "Audiosrv")
            StartupType = "Manual"
            State       = "Running"
        }
    }
}
```
