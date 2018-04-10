---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Prostředek DSC WindowsOptionalFeature
ms.openlocfilehash: 4cb59151d69adb2a01b7c4bdcaf0e961c24b29a6
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
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