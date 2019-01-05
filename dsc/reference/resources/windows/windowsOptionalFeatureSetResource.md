---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek Windowsoptionalfeatureset DSC
ms.openlocfilehash: c27d026e01bbb443a82112e37f1d199fb3482e49
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048133"
---
# <a name="dsc-windowsoptionalfeatureset-resource"></a>Prostředek Windowsoptionalfeatureset DSC

> Platí pro: Windows PowerShell 5.0

**WindowsOptionalFeatureSet** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro zajištění, že na cílový uzel je povolené volitelné funkce.
Tento prostředek je [složený prostředek](../../../resources/authoringResourceComposite.md) , která volá [prostředek WindowsOptionalFeature](windowsOptionalFeatureResource.md) pro každou součást podle `Name` vlastnost.

Pokud chcete nakonfigurovat několik volitelných funkcí Windows do stejného stavu, použijte tento prostředek.

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
| Name| Určuje název funkce, které chcete zajistit jsou zapnutá nebo vypnutá.|
| Zkontrolujte| Určuje, zda jsou povoleny funkce. K zajištění, že funkce jsou povolené, nastavte tuto vlastnost na "Zapnout" Ujistěte se, že funkce je zakázáno, nastavte vlastnost na "Zakázat".|
| Zdroj| Není implementováno.|
| NoWindowsUpdateCheck| Určuje, zda DISM kontaktuje Windows Update (WU) při hledání pro zdrojové soubory k povolení funkcí. Pokud $true, DISM nekontaktuje WU.|
| RemoveFilesOnDisable| Nastavte na **$true** odebrat všechny soubory spojené s funkcemi, když jsou zakázány (to znamená, když **Ujistěte se, že** je nastavena na "Chybí").|
| ÚroveňProtokolu| Maximální úroveň výstupu zobrazeného v protokolech. Přípustné hodnoty jsou: "ErrorsOnly" (pouze chyby se protokolují), "ErrorsAndWarning" (chyby a upozornění se protokolují) a "ErrorsAndWarningAndInformation" (chyby, upozornění a informace o ladění jsou protokolovány).|
| LogPath| Cesta k souboru protokolu, ve kterém chcete protokolovat operace poskytovatele prostředků.|
| DependsOn| Určuje, že konfigurace jiný prostředek musí spustit před konfigurací tento prostředek. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|
