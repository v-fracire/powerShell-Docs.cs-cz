---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: WindowsOptionalFeatureSet prostředek DSC
ms.openlocfilehash: 3329e0d0f1988a2ee20eb848da943ff1b22bd4df
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-windowsoptionalfeatureset-resource"></a>WindowsOptionalFeatureSet prostředek DSC

> Platí pro: Prostředí Windows PowerShell 5.0

**WindowsOptionalFeatureSet** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro Ujistěte se, že jsou na cílový uzel povolené volitelné funkce.
Tento prostředek je [složené prostředků](authoringResourceComposite.md) , který volá [WindowsOptionalFeature prostředků](windowsOptionalFeatureResource.md) pro každou funkci zadaný v `Name` vlastnost.

Pokud chcete nakonfigurovat počet volitelné funkce systému Windows do stejného stavu, použijte tento prostředek.

## <a name="syntax"></a>Syntaxe

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Source = [string] ]
    [ RemoveFilesOnDisable = [bool] ]
    [ LogPath = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| Název| Určuje název funkce, které chcete zajistit jsou zapnutá nebo vypnutá.|
| Ujistěte se| Určuje, jestli jsou povolené funkce. K zajištění, že funkce jsou povolené, nastavte tuto vlastnost možnost povolit"k zajištění, že jsou zakázány funkce, nastavte vlastnost na"Zakázat".|
| Zdroj| Není implementováno.|
| NoWindowsUpdateCheck| Určuje, zda DISM kontaktuje Windows Update (WU) při vyhledávání pro zdrojové soubory k povolení funkce. Pokud $true, DISM nebude kontaktovat služby WU.|
| RemoveFilesOnDisable| Nastavte na **$true** odebrat všechny soubory spojené s funkcí, když jsou zakázány (to znamená, když **zajistěte, aby** je nastaven na "Chybí").|
| ÚroveňProtokolu| Maximální úroveň výstupu zobrazeného v protokolech. Možné hodnoty jsou: "ErrorsOnly" (jsou protokolovány pouze chyby), "ErrorsAndWarning" (chyby a upozornění přihlášení) a "ErrorsAndWarningAndInformation" (chyby, upozornění a informace o ladění přihlášeni).|
| LogPath| Cesta k souboru protokolu, kam chcete poskytovatele prostředků do protokolu operaci.|
| dependsOn| Určuje, že konfigurace jiný prostředek musí spustit předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|