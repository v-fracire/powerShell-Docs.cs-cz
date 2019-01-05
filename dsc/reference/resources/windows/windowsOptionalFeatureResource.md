---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek WindowsOptionalFeature DSC
ms.openlocfilehash: 390caefd2ad190afc651b22ed1beb5cf1d604527
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048147"
---
# <a name="dsc-windowsoptionalfeature-resource"></a>Prostředek WindowsOptionalFeature DSC

> Platí pro: Windows PowerShell 5.0

**WindowsOptionalFeature** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro zajištění, že na cílový uzel je povolené volitelné funkce.

## <a name="syntax"></a>Syntaxe

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Source = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ RemoveFilesOnDisable = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| Name| Určuje název funkce, která budete muset zajistit, aby povolený nebo zakázaný.|
| Zkontrolujte| Určuje, zda je povolena funkce. K zajištění, že funkce je povolená, nastavte tuto vlastnost na "Zapnout" Ujistěte se, že je zakázaná, nastavte vlastnost na "Zakázat".|
| Zdroj| Není implementováno.|
| NoWindowsUpdateCheck| Určuje, zda DISM kontaktuje Windows Update (WU) při hledání pro zdrojové soubory pro povolení funkce. Pokud $true, DISM nekontaktuje WU.|
| RemoveFilesOnDisable| Nastavte na **$true** odebrat všechny soubory přidružené k této funkci, když je zakázaný (to znamená, když **Ujistěte se, že** je nastavena na "Chybí").|
| ÚroveňProtokolu| Maximální úroveň výstupu zobrazeného v protokolech. Přípustné hodnoty jsou: "ErrorsOnly" (pouze chyby se protokolují), "ErrorsAndWarning" (chyby a upozornění se protokolují) a "ErrorsAndWarningAndInformation" (chyby, upozornění a informace o ladění jsou protokolovány).|
| LogPath| Cesta k souboru protokolu, ve kterém chcete protokolovat operace poskytovatele prostředků.|
| DependsOn| Určuje, že konfigurace jiný prostředek musí spustit před konfigurací tento prostředek. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|