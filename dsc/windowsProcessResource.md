---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: WindowsProcess prostředek DSC
ms.openlocfilehash: 236a48fd4449a96f2297c152bce65253dd2fd08d
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-windowsprocess-resource"></a>WindowsProcess prostředek DSC

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

**WindowsProcess** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro konfiguraci procesů na cílový uzel.

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
|  Vlastnost  |  Popis   |
|---|---|
| Argumenty| Určuje řetězec argumenty předání do procesu jako-je. Pokud potřebujete předání několik argumentů, uložili je na tento řetězec.|
| Cesta| Cesta ke spustitelnému souboru procesu. Pokud název souboru nebo spustitelný soubor (není plně kvalifikovanou cestu), prostředek DSC hledat prostředí **cesta** proměnné (`$env:Path`) najít spustitelný soubor. Pokud je hodnota této vlastnosti plně kvalifikovanou cestu, nebude používat DSC **cesta** proměnné prostředí se najít soubor a vyvolá chybu, pokud cesta neexistuje. Relativní cesty nejsou povoleny.|
| přihlašovací údaje| Určuje pověření ke spuštění procesu.|
| Ujistěte se| Označuje, pokud proces existuje. Nastavením této vlastnosti "Přítomen" Zkontrolujte, zda existuje proces. V opačném případě ji nastavte na "Chybí". Výchozí hodnota je "Dispozici".|
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je ' DependsOn = "[Typ prostředku] ResourceName"".|
| StandardErrorPath| Určuje, cesta k adresáři pro zápis standardní chybu. Všechny existující soubory budou přepsány.|
| StandardInputPath| Určuje standardní vstupní umístění.|
| StandardOutputPath| Určuje umístění pro zápis ve standardním výstupu. Všechny existující soubory budou přepsány.|
| WorkingDirectory| Určuje umístění, které se použije jako aktuální pracovní adresář pro proces.|