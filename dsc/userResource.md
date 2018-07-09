---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC uživatele
ms.openlocfilehash: 04543351df19160a2da05ccea96e5d392d8c55bf
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892521"
---
# <a name="dsc-user-resource"></a>Prostředek DSC uživatele

Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

**Uživatele** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě místních uživatelských účtů na cílovém uzlu.

## <a name="syntax"></a>Syntaxe

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
| Zakázáno| Označuje, zda je účet povolen. Tuto vlastnost nastavte na `$true` zajistit, že tento účet je zakázaný a nastavte ho na `$false` ujistěte, že je povolena.|
| Zkontrolujte| Určuje, jestli účet existuje. Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že existuje účet a nastavte ho na "Chybí" Ujistěte se, že účet neexistuje.|
| Jméno a příjmení| Představuje řetězec s úplný název, který chcete použít pro uživatelský účet.|
| Heslo| Určuje heslo, které chcete použít pro tento účet. |
| PasswordChangeNotAllowed| Označuje, pokud uživatel může změnit heslo. Tuto vlastnost nastavte na `$true` zajistit, že uživatel nemůže změnit heslo a nastavte ho na `$false` aby uživatel mohl změnit heslo. Výchozí hodnota je `$false`.|
| PasswordChangeRequired| Označuje, pokud uživatel musí změnit heslo při příštím přihlašování. Tuto vlastnost nastavte na `$true` Pokud musí uživatel změnit heslo. Výchozí hodnota je `$true`.|
| PasswordNeverExpires| Označuje, pokud vyprší platnost hesla. K zajištění, že heslo pro tento účet nikdy nevyprší, nastavte tuto vlastnost na `$true`a nastavte ho na `$false` Pokud vyprší platnost hesla. Výchozí hodnota je `$false`.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|

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