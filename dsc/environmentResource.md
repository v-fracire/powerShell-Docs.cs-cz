---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Prostředek DSC prostředí
ms.openlocfilehash: 023ecf4cc2e3f553770d9c49a94b6e903e560b01
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34187295"
---
# <a name="dsc-environment-resource"></a>Prostředek DSC prostředí

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

__Prostředí__ prostředek v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě systémových proměnných prostředí.

## <a name="syntax"></a>Syntaxe
``` mof
Environment [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ Path = [bool] ]
    [ DependsOn = [string[]] ]
    [ Value = [string] ]
}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| Název| Určuje název proměnné prostředí, pro které chcete zajistit určitý stav.|
| Ujistěte se| Určuje, jestli existuje proměnné. Tuto vlastnost nastavit na __přítomen__ vytvoření proměnné prostředí, pokud neexistuje nebo k zajištění, že jeho hodnota odpovídá, co je zajišťováno prostřednictvím __hodnotu__ vlastnost Pokud proměnnou již existuje. Nastavte ji na __chybí__ odstranit proměnnou, pokud existuje.|
| Cesta| Definuje proměnnou prostředí, který je konfigurován. Tuto vlastnost nastavit na __$true__ -li proměnná __cesta__ proměnné; v opačném nastavte ji na __$false__. Výchozí hodnota je __$false__. Pokud je proměnná konfigurován __cesta__ proměnné, hodnota poskytnutá prostřednictvím __hodnotu__ vlastnost bude připojeno k stávající hodnotu.|
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|
| Hodnota| Hodnota pro přiřazení k proměnné prostředí.|

## <a name="example"></a>Příklad

Následující příklad zajišťuje, že __TestEnvironmentVariable__ existuje a má hodnotu __Testovací_hodnota__. Pokud není přítomen, vytvoří se.

```powershell
Environment EnvironmentExample
{
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Name = "TestEnvironmentVariable"
    Value = "TestValue"
}
```