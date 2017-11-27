---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
description: "Poskytuje mechanismus ke správě místních skupin na cílový uzel."
title: "GroupSet prostředek DSC"
ms.openlocfilehash: 0907a968bfc660adc873c28e8be6572d1d5cb993
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-groupset-resource"></a>GroupSet prostředek DSC

> Platí pro: Windows prostředí Windows PowerShell 5.0

**GroupSet** prostředek v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě místních skupin na cílový uzel. Tento prostředek je [složené prostředků](authoringResourceComposite.md) , který volá [skupiny prostředků](groupResource.md) pro každou skupinu zadaný v `GroupName` parametr.

Pokud chcete přidat nebo odebrat stejný seznam členů do více než jedné skupiny, odeberte více než jedné skupiny nebo přidat více než jednu skupinu s stejný seznam členů, použijte tento prostředek.

##<a name="syntax"></a>Syntaxe ##
```
Group [string] #ResourceName
{
    GroupName = [string[]]
    [ Ensure = [string] { Absent | Present }  ]
    [ MembersToInclude = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   | 
|---|---| 
| Název skupiny| Názvy skupin, pro které chcete zajistit určitý stav.| 
| MembersToExclude| Pomocí této vlastnosti se odebrat členy ze stávajícího členství skupin. Hodnota této vlastnosti je pole řetězce ve formátu *domény*\\*uživatelské jméno*. Pokud tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost. Tím dojde k chybě.| 
| přihlašovací údaje| Přihlašovací údaje potřebné pro přístup k vzdálené prostředky. **Poznámka:**: Tento účet musí mít příslušná oprávnění služby Active Directory přidat všechny jiné než místní účty do skupiny; jinak dojde k chybě.
| Ujistěte se| Určuje, zda existují skupiny. Nastavením této vlastnosti "Chybí" zajistit, že skupiny nejsou k dispozici. Nastavení jej do "K dispozici" (výchozí hodnota) zajišťuje, že existují skupiny.| 
| Členové| Pomocí této vlastnosti můžete nahradit členství v aktuální skupině zadaný členy. Hodnota této vlastnosti je pole řetězce ve formátu *domény*\\*uživatelské jméno*. Pokud tuto vlastnost nastavit v konfiguraci, nepoužívejte buď **MembersToExclude** nebo **MembersToInclude** vlastnost. Tím dojde k chybě.| 
| MembersToInclude| Postup přidání členů do stávajícího členství skupiny pomocí této vlastnosti. Hodnota této vlastnosti je pole řetězce ve formátu *domény*\\*uživatelské jméno*. Pokud tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost. Tím dojde k chybě.| 
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je ' DependsOn = "[ Typ prostředku] ResourceName"".| 

## <a name="example-1"></a>Příklad 1

Následující příklad ukazuje, jak zajistit, že jsou k dispozici dvě skupiny s názvem "myGroup" a "myOtherGroup". 

```powershell
configuration GroupSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {
        GroupSet GroupSetTest
        {
            GroupName        = @("myGroup", "myOtherGroup")
            Ensure           = "Present"
            MembersToInclude = @("contoso\alice", "contoso\bob")
            MembersToExclude = $("contoso\john")
            Credential       = Get-Credential
        }
    }
}
$cd = @{
    AllNodes = @(
        @{
            NodeName                    = 'localhost'
            PSDscAllowPlainTextPassword = $true
            PSDscAllowDomainUser        = $true
        }
    )
}


GroupSetTest -ConfigurationData $cd
```

>**Poznámka:** tento příklad používá pro jednoduchost přihlašovací údaje ve formátu prostého textu. Informace o tom, jak šifrování přihlašovacích údajů v konfiguračním souboru MOF najdete v tématu [zabezpečení souboru MOF](secureMOF.md).


