---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředek DSC služby"
ms.openlocfilehash: a549530edc19496a68c036fecbd18b0072cc6d74
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-service-resource"></a>Prostředek DSC služby

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0


**Služby** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě služeb na cílový uzel.

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
| Název| Určuje název služby. Všimněte si, že v některých případech se to neliší od zobrazovaný název. Můžete získat seznam služeb a jejich aktuálního stavu pomocí rutiny Get-Service.| 
| BuiltInAccount| Určuje účet přihlášení, který chcete použít pro službu. Jsou hodnoty, které jsou povoleny pro tuto vlastnost: **LocalService**, **LocalSystem**, a **NetworkService**.| 
| přihlašovací údaje| Určuje pověření pro účet, který služba bude spuštěna pod. Tato vlastnost a __BuiltinAccount__ vlastnost nelze použít společně.| 
| dependsOn| Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.| 
| StartupType| Označuje typ spuštění služby. Jsou hodnoty, které jsou povoleny pro tuto vlastnost: **automatické**, **zakázané**, a **ruční**| 
| Stav| Označuje stav, který chcete pro službu zajistit.| 
| Popis | Určuje popis cílovou službu.| 
| DisplayName | Určuje zobrazovaný název cílové služby.| 
| Ujistěte se | Určuje, zda cílová služba existuje v systému. Tuto vlastnost nastavit na **chybí** zajistit, že cílová služba neexistuje. Jeho nastavení na hodnotu **přítomen** (výchozí hodnota) zajišťuje, že cílová služba existuje.|
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

