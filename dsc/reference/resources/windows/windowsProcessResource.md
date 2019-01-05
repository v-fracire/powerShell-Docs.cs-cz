---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek Windowsprocess DSC
ms.openlocfilehash: cee93ab283ded407d6e032161125aa6d6ac98827
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048152"
---
# <a name="dsc-windowsprocess-resource"></a>Prostředek Windowsprocess DSC

_Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0_

**WindowsProcess** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro konfiguraci procesů na cílový uzel.

## <a name="syntax"></a>Syntaxe

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ DependsOn = [string[]] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]
    [ StandardOutputPath = [string] ]
    [ WorkingDirectory = [string] ]
}
```

## <a name="properties"></a>Properties

| Vlastnost | Popis |
| --- | --- |
| Argumenty| Určuje řetězec argumenty budou předány procesu jako-je. Pokud je potřeba předat několik argumentů, vytvořte z nich všechny v tomto řetězci.|
| Cesta| Cesta ke spustitelnému souboru procesu. Pokud tento soubor název spustitelného souboru (není plně kvalifikovanou cestu), prostředek DSC bude hledat prostředí **cesta** proměnné (`$env:Path`) spustitelný soubor se nenašel. Pokud je hodnota této vlastnosti plně kvalifikovanou cestu, nebudeme je používat DSC **cesta** proměnnou prostředí, aby našli požadovaný soubor a vyvolá chybu, pokud cesta neexistuje. Relativní cesty nejsou povoleny.|
| Přihlašovací údaje| Určuje přihlašovací údaje pro spuštění procesu.|
| Zkontrolujte| Určuje, jestli proces existuje. Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že proces existuje. Jinak ji nastavte na "Chybí". Výchozí hodnota je "K dispozici".|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"` .|
| StandardErrorPath| Určuje cestu k adresáři zapsat standardní chybu. Všechny existující soubory budou přepsány.|
| StandardInputPath| Označuje standardní vstupní umístění.|
| StandardOutputPath| Určuje umístění pro zápis ve standardním výstupu. Všechny existující soubory budou přepsány.|
| WorkingDirectory| Určuje umístění, které se použije jako aktuální pracovní adresář pro proces.|