---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: ProcessSet prostředek DSC
ms.openlocfilehash: d3c7383da5fd10580612527465ab621004ee7269
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-windowsprocess-resource"></a>WindowsProcess prostředek DSC

> Platí pro: Prostředí Windows PowerShell 5.0

**ProcessSet** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro konfiguraci procesů na cílový uzel. Tento prostředek je [složené prostředků](authoringResourceComposite.md) , který volá [WindowsProcess prostředků](windowsProcessResource.md) pro každou skupinu zadaný v `GroupName` parametr.

## <a name="syntax"></a>Syntaxe

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ StandardOutputPath = [string] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]
    [ WorkingDirectory = [string] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Properties
|  Vlastnost  |  Popis   |
|---|---|
| Argumenty| Řetězec, který obsahuje argumenty, které mají být předána do procesu jako-je. Pokud potřebujete předání několik argumentů, uložili je na tento řetězec.|
| Cesta| Cesty k procesu spustitelné soubory. Pokud jsou názvy spustitelné soubory (plně kvalifikovaný cest), prostředek DSC hledat prostředí **cesta** proměnné (`$env:Path`) k vyhledání soubory. Pokud jsou hodnoty této vlastnosti úplné cesty, nebude používat DSC **cesta** proměnnou prostředí nalézt soubory a vyvolá chybu, pokud neexistuje žádné cesty. Relativní cesty nejsou povoleny.|
| přihlašovací údaje| Určuje pověření ke spuštění procesu.|
| Ujistěte se| Určuje, zda existuje procesy. Nastavením této vlastnosti "Přítomen" Zkontrolujte, zda existuje proces. V opačném případě ji nastavte na "Chybí". Výchozí hodnota je "Dispozici".|
| StandardErrorPath| Cesta, do které procesy standardní Chyba zápisu. Všechny existující soubory budou přepsány.|
| StandardInputPath| Datový proud, ze kterého přijímá proces standardní vstup.|
| StandardOutputPath| Cesta souboru, do které procesy zápisu standardní výstup. Všechny existující soubory budou přepsány.|
| WorkingDirectory| Umístění použít jako aktuální pracovní adresář pro procesy.|
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba **ResourceName** a její typ je **_ResourceType**, syntaxe pro používání této vlastnosti je ' DependsOn = "[Typ prostředku] ResourceName"".|