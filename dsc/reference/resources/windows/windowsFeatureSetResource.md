---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek Windowsfeatureset DSC
ms.openlocfilehash: 8b7c7e72dd58459bd19cb723e5790a82841515c0
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048116"
---
# <a name="dsc-windowsfeatureset-resource"></a>Prostředek Windowsfeatureset DSC

> Platí pro: Windows PowerShell 5.0

**WindowsFeatureSet** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro zajištění, že role a funkce přidávají a odebírají na cílový uzel.
Tento prostředek je [složený prostředek](../../../resources/authoringResourceComposite.md) , která volá [prostředek WindowsFeature](windowsfeatureResource.md) pro každou součást podle `Name` vlastnost.

Pokud chcete konfigurovat řadu funkcí Windows do stejného stavu, použijte tento prostředek.

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
| Name| Názvy rolí nebo funkcí, které chcete zajistit přidávají a odebírají. To je stejný jako **název** vlastnost [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) rutiny a ne zobrazovaným názvem rolí nebo funkcí.|
| Přihlašovací údaje| Pověření, které slouží k přidání nebo odebrání rolí nebo funkcí.|
| Zkontrolujte| Označuje, zda jsou přidány role nebo funkce. K zajištění, že role nebo funkce přidání, nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že role nebo funkce, jsou odebrány, nastavte vlastnost na "Chybí".|
| IncludeAllSubFeature| Tuto vlastnost nastavte na **$true** zahrnout všechny požadované podfunkce s funkcí, které zadáte **název** vlastnost.|
| LogPath| Cesta k souboru protokolu, ve kterém chcete protokolovat operace poskytovatele prostředků.|
| DependsOn| Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|
| Zdroj| Určuje umístění zdrojového souboru pro použití pro instalaci, v případě potřeby.|

## <a name="example"></a>Příklad

Následující konfigurace zajistí, že **Webový Server** (IIS) a **SMTP Server** funkce a všechny podfunkce jednotlivých, jsou nainstalované.

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
