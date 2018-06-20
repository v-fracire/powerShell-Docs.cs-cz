---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: WindowsFeatureSet prostředek DSC
ms.openlocfilehash: 582f9b1f439056118680f6f814d2c202d0e823be
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34186724"
---
# <a name="dsc-windowsfeatureset-resource"></a>WindowsFeatureSet prostředek DSC

> Platí pro: Prostředí Windows PowerShell 5.0

**WindowsFeatureSet** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro Ujistěte se, že role a funkce se přidají nebo odeberou na cílový uzel.
Tento prostředek je [složené prostředků](authoringResourceComposite.md) , který volá [WindowsFeature prostředků](windowsfeatureResource.md) pro každou funkci zadaný v `Name` vlastnost.

Pokud chcete konfigurovat řadu funkcí systému Windows do stejného stavu, použijte tento prostředek.

## <a name="syntax"></a>Syntaxe

```
WindowsFeatureSet [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Absent | Present }  ]
    [ Source = [string] ]
    [ IncludeAllSubFeature = [bool] ]
    [ Credential = [PSCredential] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| Název| Názvy rolí nebo funkcí, které chcete zajistit přidání nebo odebrání. Je to stejné jako **název** vlastnost [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) rutiny a ne zobrazovaným názvem rolí nebo funkcí.|
| přihlašovací údaje| Pověření, který se má použít k přidání nebo odebrání rolí nebo funkcí.|
| Ujistěte se| Určuje, zda jsou přidány rolí nebo funkcí. Zajistit, že role nebo funkce jsou přidané, nastavte tuto vlastnost "Přítomen" zajistit, že jsou odebrány rolí nebo funkcí, nastavte vlastnost na "Chybí".|
| IncludeAllSubFeature| Tuto vlastnost nastavit na **$true** zahrnout všechny požadované jejích s funkcí, které zadáte pomocí **název** vlastnost.|
| LogPath| Cesta k souboru protokolu, kam chcete poskytovatele prostředků do protokolu operaci.|
| dependsOn| Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|
| Zdroj| Určuje umístění zdrojového souboru pro instalaci, v případě potřeby.|

## <a name="example"></a>Příklad

Následující konfigurace zajišťuje, že **Webový Server** (IIS) a **SMTP Server** funkce a všechny podfunkce jednotlivých, jsou nainstalované.

```powershell
configuration FeatureSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        WindowsFeatureSet WindowsFeatureSetExample
        {
            Name                    = @("SMTP-Server", "Web-Server")
            Ensure                  = 'Present'
            IncludeAllSubFeature    = $true
        }
    }
}
```