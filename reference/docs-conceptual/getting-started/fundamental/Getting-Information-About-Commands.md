---
ms.date: 08/27/2018
keywords: rutiny prostředí PowerShell
title: Získání informací o příkazech
ms.assetid: 56f8e5b4-d97c-4e59-abbe-bf13e464eb0d
ms.openlocfilehash: 7af83e3a0e776d96e580b442430357b4ea063a72
ms.sourcegitcommit: c170a1608d20d3c925d79c35fa208f650d014146
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/31/2018
ms.locfileid: "43353166"
---
# <a name="getting-information-about-commands"></a><span data-ttu-id="7e686-103">Získání informací o příkazech</span><span class="sxs-lookup"><span data-stu-id="7e686-103">Getting information about commands</span></span>

<span data-ttu-id="7e686-104">PowerShell `Get-Command` zobrazuje příkazy, které jsou k dispozici v aktuální relaci.</span><span class="sxs-lookup"><span data-stu-id="7e686-104">The PowerShell `Get-Command` displays commands that are available in your current session.</span></span>
<span data-ttu-id="7e686-105">Při spuštění `Get-Command` rutiny, vypadá podobně jako následující výstup:</span><span class="sxs-lookup"><span data-stu-id="7e686-105">When you run the `Get-Command` cmdlet, you see something similar to the following output:</span></span>

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

<span data-ttu-id="7e686-106">To mnohem výstup vypadá podobně jako výstup s nápovědou z **cmd.exe**: tabulkové souhrn vnitřních příkazů.</span><span class="sxs-lookup"><span data-stu-id="7e686-106">This output looks a lot like the Help output of **cmd.exe**: a tabular summary of internal commands.</span></span> <span data-ttu-id="7e686-107">V výňatek z `Get-Command` příkaz výstupu vidíte výše, každý příkaz, zobrazí se CommandType rutiny.</span><span class="sxs-lookup"><span data-stu-id="7e686-107">In the excerpt of the `Get-Command` command output shown above, every command shown has a CommandType of Cmdlet.</span></span> <span data-ttu-id="7e686-108">Rutina je typ vnitřní příkaz Powershellu.</span><span class="sxs-lookup"><span data-stu-id="7e686-108">A cmdlet is PowerShell's intrinsic command type.</span></span> <span data-ttu-id="7e686-109">Tento typ odpovídá zhruba příkazů, jako jsou `dir` a `cd` v **cmd.exe** nebo integrované příkazy prostředí Unix, jako je bash.</span><span class="sxs-lookup"><span data-stu-id="7e686-109">This type corresponds roughly to commands like `dir` and `cd` in **cmd.exe** or the built-in commands of Unix shells like bash.</span></span>

<span data-ttu-id="7e686-110">`Get-Command` Rutina má **syntaxe** parametr, který vrátí syntaxe jednotlivých rutin.</span><span class="sxs-lookup"><span data-stu-id="7e686-110">The `Get-Command` cmdlet has a **Syntax** parameter that returns syntax of each cmdlet.</span></span> <span data-ttu-id="7e686-111">Následující příklad ukazuje, jak získat syntaxe `Get-Help` rutiny:</span><span class="sxs-lookup"><span data-stu-id="7e686-111">The following example shows how to get the syntax of the `Get-Help` cmdlet:</span></span>

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

## <a name="displaying-available-command-by-type"></a><span data-ttu-id="7e686-112">Zobrazení dostupných příkazových podle typu</span><span class="sxs-lookup"><span data-stu-id="7e686-112">Displaying available command by type</span></span>

<span data-ttu-id="7e686-113">`Get-Command` Příkaz vypíše pouze rutiny v aktuální relaci.</span><span class="sxs-lookup"><span data-stu-id="7e686-113">The `Get-Command` command lists only the cmdlets in the current session.</span></span> <span data-ttu-id="7e686-114">Prostředí PowerShell skutečně podporuje několik dalších typů příkazy:</span><span class="sxs-lookup"><span data-stu-id="7e686-114">PowerShell actually supports several other types of commands:</span></span>

- <span data-ttu-id="7e686-115">Aliasy</span><span class="sxs-lookup"><span data-stu-id="7e686-115">Aliases</span></span>
- <span data-ttu-id="7e686-116">Funkce</span><span class="sxs-lookup"><span data-stu-id="7e686-116">Functions</span></span>
- <span data-ttu-id="7e686-117">Skripty</span><span class="sxs-lookup"><span data-stu-id="7e686-117">Scripts</span></span>

<span data-ttu-id="7e686-118">Externí spustitelné soubory nebo soubory, které mají obslužné rutiny typu registrovaný typ souboru, adaptéry taky klasifikované jako příkazy.</span><span class="sxs-lookup"><span data-stu-id="7e686-118">External executable files, or files that have a registered file type handler, are also classified as commands.</span></span>

<span data-ttu-id="7e686-119">Pokud chcete získat všechny příkazy v relaci, zadejte:</span><span class="sxs-lookup"><span data-stu-id="7e686-119">To get all commands in the session, type:</span></span>

```powershell
Get-Command *
```

<span data-ttu-id="7e686-120">Tento seznam obsahuje externích příkazů v cestách pro vyhledávání, tak může obsahovat tisíců položek.</span><span class="sxs-lookup"><span data-stu-id="7e686-120">This list includes external commands in your search path so it can contain thousands of items.</span></span>
<span data-ttu-id="7e686-121">Je další užitečné podívat se na omezenou sadu příkazů.</span><span class="sxs-lookup"><span data-stu-id="7e686-121">It is more useful to look at a reduced set of commands.</span></span>

> [!NOTE]
> <span data-ttu-id="7e686-122">Hvězdička (\*) se používá pro porovnávání v argumentech příkazového prostředí PowerShell se zástupnými znaky.</span><span class="sxs-lookup"><span data-stu-id="7e686-122">The asterisk (\*) is used for wildcard matching in PowerShell command arguments.</span></span> <span data-ttu-id="7e686-123">\* Znamená "odpovídat jeden nebo více znaky".</span><span class="sxs-lookup"><span data-stu-id="7e686-123">The \* means "match one or more of any characters".</span></span> <span data-ttu-id="7e686-124">Můžete zadat `Get-Command a*` najít všechny příkazy, které začínají písmenem "a".</span><span class="sxs-lookup"><span data-stu-id="7e686-124">You can type `Get-Command a*` to find all commands that begin with the letter "a".</span></span> <span data-ttu-id="7e686-125">Na rozdíl od porovnávání se zástupnými znaky v **cmd.exe**, Powershellu zástupných znaků se také Porovná tečku.</span><span class="sxs-lookup"><span data-stu-id="7e686-125">Unlike wildcard matching in **cmd.exe**, PowerShell's wildcard will also match a period.</span></span>

<span data-ttu-id="7e686-126">Použití **CommandType** parametr `Get-Command` zobrazíte nativní příkazy z ostatních typů.</span><span class="sxs-lookup"><span data-stu-id="7e686-126">Use the **CommandType** parameter of `Get-Command` to get native commands of other types.</span></span>
<span data-ttu-id="7e686-127">.</span><span class="sxs-lookup"><span data-stu-id="7e686-127">cmdlet.</span></span>

<span data-ttu-id="7e686-128">Chcete-li získat aliasy příkazů, které jsou přiřazené zástupné názvy příkazů, zadejte:</span><span class="sxs-lookup"><span data-stu-id="7e686-128">To get command aliases, which are the assigned nicknames of commands, type:</span></span>

```powershell
Get-Command -CommandType Alias
```

<span data-ttu-id="7e686-129">Chcete-li získat funkce v aktuální relaci, zadejte:</span><span class="sxs-lookup"><span data-stu-id="7e686-129">To get the functions in the current session, type:</span></span>

```powershell
Get-Command -CommandType Function
```

<span data-ttu-id="7e686-130">Zobrazíte skripty v cestách pro vyhledávání na Powershellu, zadejte:</span><span class="sxs-lookup"><span data-stu-id="7e686-130">To display scripts in PowerShell's search path, type:</span></span>

```powershell
Get-Command -CommandType Script
```