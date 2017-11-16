---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Získání informací o příkazech"
ms.assetid: 56f8e5b4-d97c-4e59-abbe-bf13e464eb0d
ms.openlocfilehash: 98e449110860ea81939d6ec0b7b1a8534a2da2aa
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="getting-information-about-commands"></a>Získání informací o příkazech
Prostředí Windows PowerShell **Get-Command** rutiny získá všechny příkazy, které jsou k dispozici v aktuální relaci. Pokud zadáte **Get-Command** na řádku prostředí Windows PowerShell, zobrazí se výstup podobný následujícímu:

```
PS> Get-Command
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
Cmdlet          Add-Member                      Add-Member [-MemberType] <PS...
...
```

To mnohem výstup vypadá jako výstup nápovědy Cmd.exe: tabulkový souhrn interní příkazy. V výňatek ze **Get-Command** příkaz uvedené výše, každý příkaz zobrazí výstup má CommandType rutiny. Rutiny je typ vnitřní příkazu prostředí Windows PowerShell - typ, který odpovídá zhruba na **dir** a **cd** Cmd.exe a built-ins v součásti pro UNIX, jako je například BASH příkazy.

Ve výstupu **Get-Command** příkaz ukončení všech definic se třemi tečkami (...) k označení, že prostředí PowerShell nemůže zobrazit celý obsah v dostupného místa. Když prostředí Windows PowerShell zobrazí výstup, způsobí, že výstup jako text a pak ho tak, aby data řádně nevejde se do okna uspořádá. Se věnuje to později v části na formátování.

**Get-Command** rutina má **syntaxe** parametr, který získá syntaxe každou rutinu. Získání syntaxe rutiny Get-Help, použijte následující příkaz:

**Get-Help Get-Command-syntaxe**

```
Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Full] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Detailed] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Examples] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Parameter <String>] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]
```

### <a name="displaying-available-command-types"></a>Zobrazení dostupných příkazových typů
**Get-Command** příkaz nezobrazovat každý příkaz, který je k dispozici v prostředí Windows PowerShell. Místo toho **Get-Command** příkaz vypíše jenom rutiny v aktuální relaci. Prostředí Windows PowerShell ve skutečnosti podporuje několik typů příkazů. Aliasy, funkcí a skriptů jsou také příkazy prostředí Windows PowerShell, i když nejsou popsané v podrobností v Průvodci uživatele Windows PowerShell. Externí soubory, které jsou spustitelné nebo obslužná rutina typ zaregistrované sdílené, jsou také klasifikovány jako příkazy.

Chcete-li získat všechny příkazy v relaci, zadejte:

```
Get-Command *
```

Tento seznam zahrnuje externí soubory v cestě vyhledávání, a proto může obsahovat tisíce položek. Je více užitečné prohlédnout si omezenou sadu příkazů.

Nativní příkazy jiné typy, použijte **CommandType** parametr **Get-Command** rutiny.

> [!NOTE]
> Hvězdička (\*) se používá pro porovnávání v prostředí Windows PowerShell argumenty příkazu se zástupnými znaky. \* Znamená "odpovídat jeden nebo více znaky". Můžete zadat **Get-Command\&#42;** najít všechny příkazy, které začínají písmenem "a". Na rozdíl od v Cmd.exe porovnávání se zástupnými znaky bude odpovídat zástupné prostředí Windows PowerShell taky období.

Chcete-li získat aliasy příkazů, které jsou přiřazené zástupné názvy příkazů, zadejte:

```
Get-Command -CommandType Alias
```

Chcete-li získat funkce v aktuální relaci, zadejte:

```
Get-Command -CommandType Function
```

Chcete-li zobrazit skriptů v prostředí Windows PowerShell cesty pro hledání, zadejte:

```
Get-Command -CommandType Script
```

