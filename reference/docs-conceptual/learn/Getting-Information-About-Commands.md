---
ms.date: 08/27/2018
keywords: rutiny prostředí PowerShell
title: Získání informací o příkazech
ms.assetid: 56f8e5b4-d97c-4e59-abbe-bf13e464eb0d
ms.openlocfilehash: 7af83e3a0e776d96e580b442430357b4ea063a72
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404071"
---
# <a name="getting-information-about-commands"></a>Získání informací o příkazech

PowerShell `Get-Command` zobrazuje příkazy, které jsou k dispozici v aktuální relaci.
Při spuštění `Get-Command` rutiny, vypadá podobně jako následující výstup:

```output
CommandType     Name                    Version    Source
-----------     ----                    -------    ------
Cmdlet          Add-Computer            3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Add-Content             3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Add-History             3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Add-JobTrigger          1.1.0.0    PSScheduledJob
Cmdlet          Add-LocalGroupMember    1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Add-Member              3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Add-PSSnapin            3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Add-Type                3.1.0.0    Microsoft.PowerShell.Utility
...
```

To mnohem výstup vypadá podobně jako výstup s nápovědou z **cmd.exe**: tabulkové souhrn vnitřních příkazů. V výňatek z `Get-Command` příkaz výstupu vidíte výše, každý příkaz, zobrazí se CommandType rutiny. Rutina je typ vnitřní příkaz Powershellu. Tento typ odpovídá zhruba příkazů, jako jsou `dir` a `cd` v **cmd.exe** nebo integrované příkazy prostředí Unix, jako je bash.

`Get-Command` Rutina má **syntaxe** parametr, který vrátí syntaxe jednotlivých rutin. Následující příklad ukazuje, jak získat syntaxe `Get-Help` rutiny:

```powershell
Get-Command Get-Help -Syntax
```

```output
Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Full] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Detailed] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Examples] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Parameter <String>] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]
```

## <a name="displaying-available-command-by-type"></a>Zobrazení dostupných příkazových podle typu

`Get-Command` Příkaz vypíše pouze rutiny v aktuální relaci. Prostředí PowerShell skutečně podporuje několik dalších typů příkazy:

- Aliasy
- Funkce
- Skripty

Externí spustitelné soubory nebo soubory, které mají obslužné rutiny typu registrovaný typ souboru, adaptéry taky klasifikované jako příkazy.

Pokud chcete získat všechny příkazy v relaci, zadejte:

```powershell
Get-Command *
```

Tento seznam obsahuje externích příkazů v cestách pro vyhledávání, tak může obsahovat tisíců položek.
Je další užitečné podívat se na omezenou sadu příkazů.

> [!NOTE]
> Hvězdička (\*) se používá pro porovnávání v argumentech příkazového prostředí PowerShell se zástupnými znaky. \* Znamená "odpovídat jeden nebo více znaky". Můžete zadat `Get-Command a*` najít všechny příkazy, které začínají písmenem "a". Na rozdíl od porovnávání se zástupnými znaky v **cmd.exe**, Powershellu zástupných znaků se také Porovná tečku.

Použití **CommandType** parametr `Get-Command` zobrazíte nativní příkazy z ostatních typů.
.

Chcete-li získat aliasy příkazů, které jsou přiřazené zástupné názvy příkazů, zadejte:

```powershell
Get-Command -CommandType Alias
```

Chcete-li získat funkce v aktuální relaci, zadejte:

```powershell
Get-Command -CommandType Function
```

Zobrazíte skripty v cestách pro vyhledávání na Powershellu, zadejte:

```powershell
Get-Command -CommandType Script
```