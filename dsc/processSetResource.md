---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek Processset DSC
ms.openlocfilehash: 33000786a9e17e11168b5e08c3bcfcacf3af2611
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268010"
---
# <a name="dsc-windowsprocess-resource"></a>Prostředek Windowsprocess DSC

_Platí pro: Windows PowerShell 5.0_

**ProcessSet** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro konfiguraci procesů na cílový uzel. Tento prostředek je [složený prostředek](authoringResourceComposite.md) , která volá [prostředek windowsprocess](windowsProcessResource.md) pro každou skupinu podle `GroupName` parametru.

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

| Vlastnost | Popis |
| --- | --- |
| Argumenty| Řetězec, který obsahuje argumenty budou předány procesu jako-je. Pokud je potřeba předat několik argumentů, vytvořte z nich všechny v tomto řetězci.|
| Cesta| Cesty pro spustitelné soubory procesu. Pokud se jedná se o názvy spustitelných souborů (plně kvalifikovanou cestou), prostředek DSC bude hledat prostředí **cesta** proměnné (`$env:Path`) k vyhledání souborů. Pokud jsou hodnoty této vlastnosti plně kvalifikovanou cestou, nebudeme je používat DSC **cesta** proměnnou prostředí k vyhledání souborů a vyvolá chybu, pokud neexistuje žádné cesty. Relativní cesty nejsou povoleny.|
| Přihlašovací údaje| Určuje přihlašovací údaje pro spuštění procesu.|
| Zkontrolujte| Určuje, zda existuje procesy. Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že proces existuje. Jinak ji nastavte na "Chybí". Výchozí hodnota je "K dispozici".|
| StandardErrorPath| Cesta, ke kterému procesy standardní Chyba zápisu. Všechny existující soubory budou přepsány.|
| StandardInputPath| Datový proud, ze kterého proces obdrží standardní vstup.|
| StandardOutputPath| Cestu k souboru, ke kterému procesy, které zapisují standardní výstup. Všechny existující soubory budou přepsány.|
| WorkingDirectory| Umístění použité jako aktuální pracovní adresář pro procesy.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **_ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"` .|