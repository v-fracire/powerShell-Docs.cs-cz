---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxFileLine
ms.openlocfilehash: f2a989dd3a6746948e09ba94e279c02be8ebe2de
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893293"
---
# <a name="dsc-for-linux-nxfileline-resource"></a>DSC pro Linux prostředek nxFileLine

**NxFileLine** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus k správě řádky v konfiguračním souboru v systému Linux uzlu.

## <a name="syntax"></a>Syntaxe

```
nxFileLine <string> #ResourceName
{
    FilePath = <string>
    ContainsLine = <string>
    [ DoesNotContainPattern = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Properties

|  Vlastnost |  Popis |
|---|---|
| Cesta k souboru| Úplná cesta k souboru, který má spravovat řádky v na cílový uzel.|
| ContainsLine| Řádek zajistit existuje v souboru. Tento řádek bude připojen k souboru, pokud neexistuje v souboru. **ContainsLine** je povinná, ale lze nastavit na prázdný řetězec (`ContainsLine = ""`) Pokud není potřeba.|
| DoesNotContainPattern| Vzor regulárního výrazu pro řádky, které by neměly existovat v souboru. Pro všechny řádky, které existují v souboru, které odpovídají tento regulární výraz se odebere ze souboru řádek.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Příklad

Tento příklad ukazuje použití **nxFileLine** prostředků ke konfiguraci `/etc/sudoers` souboru zajistit, aby uživatel: monuser nastavená na Ne requiretty.

```powershell
Import-DscResource -Module nx

nxFileLine DoNotRequireTTY
{
   FilePath = “/etc/sudoers”
   ContainsLine = 'Defaults:monuser !requiretty'
   DoesNotContainPattern = "Defaults:monuser[ ]+requiretty"
}
```