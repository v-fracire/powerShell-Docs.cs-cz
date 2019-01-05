---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC prostředí
ms.openlocfilehash: 2bc1600a9df32538d59efa712569b12fa9e3beee
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048131"
---
# <a name="dsc-environment-resource"></a>Prostředek DSC prostředí

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

__Prostředí__ prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě seznamu proměnných prostředí systému.

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
| Name| Určuje název proměnné prostředí, pro které chcete zajistit určitý stav.|
| Zkontrolujte| Určuje, jestli existuje proměnná. Tuto vlastnost nastavte na __k dispozici__ vytvořit proměnnou prostředí, pokud neexistuje nebo k zajištění, že její hodnota odpovídá, co je poskytována prostřednictvím __hodnotu__ vlastnost, pokud je proměnná už existuje. Nastavte ho na __chybí__ odstranit proměnnou, pokud existuje.|
| Cesta| Definuje proměnnou prostředí, který je konfigurován. Tuto vlastnost nastavte na __$true__ Pokud je proměnná __cesta__ proměnné; v opačném případě nastavte ho na __$false__. Výchozí hodnota je __$false__. Pokud je proměnná, která se právě nastavuje __cesta__ proměnné, hodnota poskytnutá prostřednictvím __hodnotu__ vlastnost se připojí k existující hodnotu.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|
| Hodnota| Hodnota, kterou chcete přiřadit k proměnné prostředí.|

## <a name="example"></a>Příklad

Následující příklad zajistí, že __TestEnvironmentVariable__ existuje a má hodnotu __Testovaci_Hodnota__. Pokud tam není, vytvoří se.

```powershell
Environment EnvironmentExample
{
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Name = "TestEnvironmentVariable"
    Value = "TestValue"
}
```