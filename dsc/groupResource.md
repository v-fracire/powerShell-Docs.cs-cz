---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředek DSC skupiny"
ms.openlocfilehash: 8a2087455a72ec1f368f890b62228b31cf4ec95a
ms.sourcegitcommit: c72c76f6ed77b3e6f26fef3e8784b157bfc19355
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/06/2018
---
# <a name="dsc-group-resource"></a>Prostředek DSC skupiny

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Skupiny prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě místních skupin na cílový uzel.

## <a name="syntax"></a>Syntaxe

```
Group [string] #ResourceName
{
    GroupName          = [string]
    [ Credential       = [PSCredential] ]
    [ Description      = [string[]] ]
    [ Ensure           = [string] { Absent | Present }  ]
    [ Members          = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ MembersToInclude = [string[]] ]
    [ DependsOn        = [string[]] ]
}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| Název skupiny| Název skupiny, pro které chcete zajistit určitý stav.|
| přihlašovací údaje| Přihlašovací údaje potřebné pro přístup k vzdálené prostředky. **Poznámka:**: Tento účet musí mít příslušná oprávnění služby Active Directory přidat všechny jiné než místní účty do skupiny; jinak, pokud dojde k chybě konfigurace se spustí na cílovém uzlu.
| Popis| Popis skupiny.|
| Ujistěte se| Označuje, pokud existuje daná skupina. Nastavením této vlastnosti "Chybí" zajistit, že skupina neexistuje. Nastavení jej do "K dispozici" (výchozí hodnota) zajišťuje, zda existuje daná skupina.|
| Členové| Pomocí této vlastnosti můžete nahradit členství v aktuální skupině zadaný členy. Hodnota této vlastnosti je pole řetězce ve formátu *domény*\\*uživatelské jméno*. Pokud tuto vlastnost nastavit v konfiguraci, nepoužívejte buď **MembersToExclude** nebo **MembersToInclude** vlastnost. Tím dojde k chybě.|
| MembersToExclude| Pomocí této vlastnosti se odebrat členy ze stávajícího členství skupiny. Hodnota této vlastnosti je pole řetězce ve formátu *domény*\\*uživatelské jméno*. Pokud tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost. Tím dojde k chybě.|
| MembersToInclude| Postup přidání členů do stávajícího členství skupiny pomocí této vlastnosti. Hodnota této vlastnosti je pole řetězce ve formátu *domény*\\*uživatelské jméno*. Pokud tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost. Tím dojde k chybě.|
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je ' DependsOn = "[ Typ prostředku] ResourceName"".|

## <a name="example-1"></a>Příklad 1

Následující příklad ukazuje, jak zajistit, že skupinu s názvem "TestGroup" chybí.

```powershell
Group GroupExample
{
    # This removes TestGroup, if present
    # To create a new group, set Ensure to "Present“
    Ensure = "Absent"
    GroupName = "TestGroup"
}
```

## <a name="example-2"></a>Příklad 2

Následující příklad ukazuje, jak přidat uživatele služby Active Directory do místní skupiny administrators v rámci prostředí s více počítači sestavení, které už používáte přihlašovací údaje pro účet místního správce.
To je také používá pro účet správce domény (po povýšení domény), potřebujeme pak převést tuto existující přihlašovací údaje pověření domény popisný.
Potom jsme do místní skupiny Administrators na členském serveru, můžete přidat uživatele domény.

```powershell
@{
    AllNodes = @(
        @{
            NodeName = '*';
            DomainName = 'SubTest.contoso.com';
         }
        @{
            NodeName = 'Box2';
            AdminAccount = 'Admin-Dave_Alexanderson'
        }
    )
}

$domain = $node.DomainName.split('.')[0]
$DCredential = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList ("$domain\$($credential.Username)", $Credential.Password)

Group AddADUserToLocalAdminGroup {
    GroupName='Administrators'
    Ensure= 'Present'
    MembersToInclude= "$domain\$($Node.AdminAccount)"
    Credential = $dCredential
    PsDscRunAsCredential = $DCredential
}
```

## <a name="example-3"></a>Příklad 3

Následující příklad ukazuje, jak ověřit místní skupina, TigerTeamAdmins, na serveru TigerTeamSource.Contoso.Com neobsahuje účet konkrétní domény, Contoso\JerryG.

```powershell
Configuration SecureTigerTeamSrouce {
  Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

  Node TigerTeamSource.Contoso.Com {
    Group TigerTeamAdmins {
       GroupName        = 'TigerTeamAdmins'
       Ensure           = 'Present'
       MembersToExclude = "Contoso\JerryG"
    }
  }
}
```
