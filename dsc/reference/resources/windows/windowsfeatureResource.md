---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek WindowsFeature DSC
ms.openlocfilehash: 7a57f4b2797ab3bb202aea8b2543d1e3f14074e9
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048153"
---
# <a name="dsc-windowsfeature-resource"></a>Prostředek WindowsFeature DSC

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

**WindowsFeature** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro zajištění, že role a funkce přidávají a odebírají na cílový uzel.

## <a name="syntax"></a>Syntaxe

```
WindowsFeature [string] #ResourceName
{
    Name = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ IncludeAllSubFeature = [bool] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ Source = [string] ]
}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| Name| Určuje název role nebo funkce, které chcete zajistit přidá nebo odebere. To je stejný jako __název__ vlastnost z [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) rutiny a nikoli zobrazovaný název role nebo funkce.|
| Přihlašovací údaje| Určuje pověření, které slouží k přidání nebo odebrání role nebo funkce.|
| Zkontrolujte| Označuje, pokud je přidána role nebo funkce. K zajištění, že role nebo funkce je přidána, nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že se odebere roli nebo funkci, nastavte vlastnost na "Chybí".|
| IncludeAllSubFeature| Tuto vlastnost nastavte na __$true__ zajistit stav všech požadovaných tyto položky se stavem funkci zadáte __název__ vlastnost.|
| LogPath| Určuje cestu k souboru protokolu, ve kterém chcete protokolovat operace poskytovatele prostředků.|
| DependsOn| Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|
| Zdroj| Určuje umístění zdrojového souboru pro použití pro instalaci, v případě potřeby.|

## <a name="example"></a>Příklad
```powershell
WindowsFeature RoleExample
{
    Ensure = "Present"
    # Alternatively, to ensure the role is uninstalled, set Ensure to "Absent"
    Name = "Web-Server" # Use the Name property from Get-WindowsFeature
}
```