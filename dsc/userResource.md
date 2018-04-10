---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Prostředek DSC uživatele
ms.openlocfilehash: 1c3efa8e3bf945c45834cbea7ddb0a6c3ffc5f45
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
#<a name="dsc-user-resource"></a>Prostředek DSC uživatele #


>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0


__Uživatele__ prostředek v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě místní uživatelské účty na cílovém uzlu.


##<a name="syntax"></a>Syntaxe ##

```
User [string] #ResourceName
{
    UserName = [string]
    [ Description = [string] ]
    [ Disabled = [bool] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ FullName = [string] ]
    [ Password = [PSCredential] ]
    [ PasswordChangeNotAllowed = [bool] ]
    [ PasswordChangeRequired = [bool] ]
    [ PasswordNeverExpires = [bool] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Properties
|  Vlastnost  |  Popis   |
|---|---|
| UserName| Určuje název účtu, pro které chcete zajistit určitý stav.|
| Popis| Určuje popis, který chcete použít pro uživatelský účet.|
| Zakázáno| Určuje, zda je povolen účet. Tuto vlastnost nastavit na __$true__ zajistit, že tento účet je zakázané a nastavte ji na __$false__ zajistit, že je povolena.|
| Ujistěte se| Určuje, jestli účet existuje. Nastavením této vlastnosti "Přítomen" zajistit, že existuje účet a nastavte ji na "Chybí" zajistit, že účet neexistuje.|
| FullName| Představuje řetězec s úplný název, který chcete použít pro uživatelský účet.|
| Heslo| Určuje heslo, které chcete použít pro tento účet. |
| PasswordChangeNotAllowed| Určuje, pokud uživatel změnit heslo. Tuto vlastnost nastavit na __$true__ zajistit, že uživatel nemůže změnit heslo a nastavte ji na __$false__ umožňuje uživatelům změnit heslo. Výchozí hodnota je __$false__.|
| PasswordChangeRequired| Označuje, pokud uživatel musí změnit heslo při příštím přihlašování. Tuto vlastnost nastavit na __$true__ Pokud musí uživatel změnit heslo. Výchozí hodnota je __$true__.|
| PasswordNeverExpires| Označuje, pokud vyprší platnost hesla. K zajištění, že heslo pro tento účet nikdy nevyprší, nastavte tuto vlastnost __$true__a nastavte ji na __$false__ Pokud vyprší platnost hesla. Výchozí hodnota je __$false__.|
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Příklad

```powershell
User UserExample
{
    Ensure = "Present"  # To ensure the user account does not exist, set Ensure to "Absent"
    UserName = "SomeName"
    Password = $passwordCred # This needs to be a credential object
    DependsOn = "[Group]GroupExample" # Configures GroupExample first
}
```