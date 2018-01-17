---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředek DSC WindowsFeature"
ms.openlocfilehash: 3dd4a9c6f11b0c76054ca3e95796cab8e709a7c6
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-windowsfeature-resource"></a>Prostředek DSC WindowsFeature

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

**WindowsFeature** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro Ujistěte se, že role a funkce se přidají nebo odeberou na cílový uzel.

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
| Název| Určuje název role nebo funkce, které chcete zajistit přidat nebo odebrat. Je to stejné jako __název__ vlastnost z [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) rutiny a nikoli zobrazovaný název role nebo funkce.| 
| přihlašovací údaje| Určuje pověření, které můžete přidat nebo odebrat roli nebo funkci.| 
| Ujistěte se| Označuje, pokud je přidána role nebo funkce. K zajištění, že je role nebo funkce přidané, nastavte tuto vlastnost "Přítomen" se ujistěte, že je odebrán roli nebo funkci, nastavte vlastnost na "Chybí".| 
| IncludeAllSubFeature| Tuto vlastnost nastavit na __$true__ zajistit stav všechny požadované položky se stavem funkci zadáte pomocí __název__ vlastnost.| 
| LogPath| Určuje cestu k souboru protokolu, kam chcete poskytovatele prostředků do protokolu operaci.| 
| dependsOn| Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.| 
| Zdroj| Určuje umístění zdrojového souboru pro instalaci, v případě potřeby.| 

## <a name="example"></a>Příklad
```powershell
WindowsFeature RoleExample
{
    Ensure = "Present" 
    # Alternatively, to ensure the role is uninstalled, set Ensure to "Absent"
    Name = "Web-Server" # Use the Name property from Get-WindowsFeature  
}
```

