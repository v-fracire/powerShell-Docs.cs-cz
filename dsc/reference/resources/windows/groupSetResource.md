---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
description: Poskytuje mechanismus ke správě místních skupin na cílový uzel.
title: Prostředek Groupset DSC
ms.openlocfilehash: afe4c4d33ac5620c411481e93d76a1f90c26deb9
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048158"
---
# <a name="dsc-groupset-resource"></a>Prostředek Groupset DSC

> Platí pro: Windows PowerShell 5.0

**GroupSet** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě místních skupin na cílový uzel. Tento prostředek je [složený prostředek](../../../resources/authoringResourceComposite.md) , která volá [skupině prostředků](groupResource.md) pro každou skupinu podle `GroupName` parametru.

Použijte tento prostředek, pokud chcete přidat nebo odebrat stejný seznam členů do více než jedné skupiny, odebrání více než jedné skupině nebo přidat více než jednu skupinu pomocí stejného seznamu členů.

## <a name="syntax"></a>Syntaxe

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
| MembersToExclude| Tuto vlastnost použijte k odebrání členů ze stávajícího členství skupin. Hodnota této vlastnosti je pole řetězců formuláře *domény*\\*uživatelské jméno*. Pokud byste tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost. Tím dojde k chybě.|
| Přihlašovací údaje| Na pověření potřebná pro přístup ke vzdáleným prostředkům. **Poznámka:**: Tento účet musí mít příslušná oprávnění služby Active Directory přidat všechny jiné než místní účty do skupiny; v opačném případě dojde k chybě.
| Zkontrolujte| Udává, zda existuje skupiny. Nastavte tuto vlastnost na "Chybí" Ujistěte se, že skupiny neexistují. Nastavení "Prezentovat" (výchozí hodnota) zajišťuje, že existují skupiny.|
| Členové| Tuto vlastnost použijte k nahrazení aktuální členství ve skupině se zadanými členy. Hodnota této vlastnosti je pole řetězců formuláře *domény*\\*uživatelské jméno*. Pokud byste tuto vlastnost nastavit v konfiguraci, nepoužívejte buď **MembersToExclude** nebo **MembersToInclude** vlastnost. Tím dojde k chybě.|
| MembersToInclude| Tuto vlastnost použijte k přidání členů do existující členství ve skupině. Hodnota této vlastnosti je pole řetězců formuláře *domény*\\*uživatelské jméno*. Pokud byste tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost. Tím dojde k chybě.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je "DependsOn ="[ ResourceName ResourceType]"".|

## <a name="example-1-ensuring-groups-are-present"></a>Příklad 1: Zajistit, že skupiny jsou k dispozici

Následující příklad ukazuje, jak zajistit, aby byly k dispozici dvě skupiny s názvem "myGroup" a "myOtherGroup".

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

> [!NOTE]
> Tento příklad používá pro jednoduchost přihlašovací údaje jako prostý text. Informace o tom, jak šifrování přihlašovacích údajů v konfiguračním souboru MOF najdete v tématu [zabezpečení souboru MOF](../../../pull-server/secureMOF.md).
