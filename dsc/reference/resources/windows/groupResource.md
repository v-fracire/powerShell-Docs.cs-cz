---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC skupiny
ms.openlocfilehash: 9894150f6f749fc23efd4ce2b155b18788557d1d
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048123"
---
# <a name="dsc-group-resource"></a>Prostředek DSC skupiny

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Skupiny prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě místních skupin na cílový uzel.

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
| Přihlašovací údaje| Na pověření potřebná pro přístup ke vzdáleným prostředkům. **Poznámka:**: Tento účet musí mít příslušná oprávnění služby Active Directory přidat všechny jiné než místní účty do skupiny; v opačném případě dojde k chybě při konfiguraci spuštění na cílovém uzlu.
| Popis| Popis skupiny.|
| Zkontrolujte| Určuje, zda skupina existuje. Nastavte tuto vlastnost na "Chybí" Ujistěte se, že skupina neexistuje. Nastavení "Prezentovat" (výchozí hodnota) zajišťuje, že tato skupina existuje.|
| Členové| Tuto vlastnost použijte k nahrazení aktuální členství ve skupině se zadanými členy. Hodnota této vlastnosti je pole řetězců formuláře *domény*\\*uživatelské jméno*. Pokud byste tuto vlastnost nastavit v konfiguraci, nepoužívejte buď **MembersToExclude** nebo **MembersToInclude** vlastnost. Tím dojde k chybě.|
| MembersToExclude| Tuto vlastnost použijte k odebrání členů z existující členství ve skupině. Hodnota této vlastnosti je pole řetězců formuláře *domény*\\*uživatelské jméno*. Pokud byste tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost. Tím dojde k chybě.|
| MembersToInclude| Tuto vlastnost použijte k přidání členů do existující členství ve skupině. Hodnota této vlastnosti je pole řetězců formuláře *domény*\\*uživatelské jméno*. Pokud byste tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost. Tím dojde k chybě.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je "DependsOn ="[ ResourceName ResourceType]"".|

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

Následující příklad ukazuje, jak přidat uživatele služby Active Directory do místní skupiny administrators v rámci testovacího prostředí s více počítači sestavení, pokud už používáte objekt PSCredential pro účet místního správce.
Jak to se také používá pro účet správce domény (po povýšení domény), následně je potřeba převést tento existující PSCredential doméně popisným přihlašovací údaje.
Pak můžeme přidat uživatele domény do místní skupiny Administrators na členský server.

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

Následující příklad ukazuje, jak zajistit místní skupina, TigerTeamAdmins, na serveru TigerTeamSource.Contoso.Com neobsahuje konkrétní doménový účet, Contoso\JerryG.

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