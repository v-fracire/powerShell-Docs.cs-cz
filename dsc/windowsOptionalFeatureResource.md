---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředek DSC WindowsOptionalFeature"
ms.openlocfilehash: 388fbe1bc430098d6680902e0b5643243fbf7f4c
ms.sourcegitcommit: 79e8f03afb8d0b0bb0a167e56464929b27f51990
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/26/2017
---
# <a name="dsc-windowsoptionalfeature-resource"></a>Prostředek DSC WindowsOptionalFeature

> Platí pro: Prostředí Windows PowerShell 5.0

**WindowsOptionalFeature** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro Ujistěte se, že jsou na cílový uzel povolené volitelné funkce.

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
| Název| Určuje název funkce, které chcete zajistit povolený nebo zakázaný.| 
| Ujistěte se| Určuje, zda je povolena funkce. K zajištění, že tato funkce je povoleno, nastavte tuto vlastnost možnost povolit"k zajištění, že tato funkce je zakázaná, nastavte vlastnost na"Zakázat".|
| Zdroj| Není implementováno.|
| NoWindowsUpdateCheck| Určuje, zda DISM kontaktuje Windows Update (WU) při vyhledávání pro zdrojové soubory pro povolení funkce. Pokud $true, DISM nebude kontaktovat služby WU.|
| RemoveFilesOnDisable| Nastavte na **$true** odebere všechny soubory přidružené k této funkci, pokud je zakázán (to znamená, když **zajistěte, aby** je nastaven na "Chybí").|
| ÚroveňProtokolu| Maximální úroveň výstupu zobrazeného v protokolech. Možné hodnoty jsou: "ErrorsOnly" (jsou protokolovány pouze chyby), "ErrorsAndWarning" (chyby a upozornění přihlášení) a "ErrorsAndWarningAndInformation" (chyby, upozornění a informace o ladění přihlášeni).|
| LogPath| Cesta k souboru protokolu, kam chcete poskytovatele prostředků do protokolu operaci.| 
| dependsOn| Určuje, že konfigurace jiný prostředek musí spustit předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.| 
 



