---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxEnvironment
ms.openlocfilehash: 763ec560faa6adaf42aef3c21c9045be95f780bc
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2018
ms.locfileid: "50225977"
---
# <a name="dsc-for-linux-nxenvironment-resource"></a>DSC pro Linux prostředek nxEnvironment

**NxEnvironment** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě seznamu proměnných prostředí systému v systému Linux uzlu.

## <a name="syntax"></a>Syntaxe

```
nxEnvironment <string> #ResourceName
{
    Name = <string>
    [ Value = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Path = <bool> }
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Properties

|  Vlastnost |  Popis |
|---|---|
| Název| Určuje název proměnné prostředí, pro které chcete zajistit určitý stav.|
| Hodnota| Hodnota, kterou chcete přiřadit k proměnné prostředí.|
| Zkontrolujte| Určuje, jestli se má zkontrolovat, zda existuje proměnná. Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že existuje proměnná. Nastavte ho na "Chybí" Ujistěte se, že proměnná neexistuje. Výchozí hodnota je "K dispozici".|
| Cesta| Definuje proměnnou prostředí, který je konfigurován. Tuto vlastnost nastavte na **$true** Pokud je proměnná **cesta** proměnné; v opačném případě nastavte ho na **$false**. Výchozí hodnota je **$false**. Pokud je proměnná, která se právě nastavuje **cesta** proměnné, hodnota poskytnutá prostřednictvím **hodnotu** vlastnost se připojí k existující hodnotu.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="additional-information"></a>Další informace

* Pokud **cesta** chybí nebo je nastavena na **$false**, proměnné prostředí jsou spravovány v `/etc/environment`. Programů nebo skriptů můžou vyžadovat konfiguraci ke zdroji `/etc/environment` souboru pro přístup k proměnným spravovaném prostředí.
* Pokud **cesta** je nastavena na **$true**, proměnné prostředí se spravuje v souboru `/etc/profile.d/DSCenvironment.sh`. Tento soubor bude vytvořen, pokud neexistuje. Pokud **Ujistěte se, že** je nastavena na "Chybí" a **cesta** je nastavena na **$true**, existující proměnné prostředí pouze se odebere z `/etc/profile.d/DSCenvironment.sh` a ne z jiných souborů.

## <a name="example"></a>Příklad

Následující příklad ukazuje způsob použití **nxEnvironment** prostředků zajistit, aby **TestEnvironmentVariable** je k dispozici a má hodnotu "Test-Value". Pokud **TestEnvironmentVariable** není k dispozici, bude vytvořen.

```
Import-DSCResource -Module nx


nxEnvironment EnvironmentExample
{
    Ensure = “Present”
    Name = “TestEnvironmentVariable”
    Value = “TestValue”
}
```