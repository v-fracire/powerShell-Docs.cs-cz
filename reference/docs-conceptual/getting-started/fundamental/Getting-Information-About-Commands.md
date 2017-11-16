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
# <a name="getting-information-about-commands"></a><span data-ttu-id="29939-103">Získání informací o příkazech</span><span class="sxs-lookup"><span data-stu-id="29939-103">Getting Information About Commands</span></span>
<span data-ttu-id="29939-104">Prostředí Windows PowerShell **Get-Command** rutiny získá všechny příkazy, které jsou k dispozici v aktuální relaci.</span><span class="sxs-lookup"><span data-stu-id="29939-104">The Windows PowerShell **Get-Command** cmdlet gets all commands that are available in your current session.</span></span> <span data-ttu-id="29939-105">Pokud zadáte **Get-Command** na řádku prostředí Windows PowerShell, zobrazí se výstup podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="29939-105">When you type **Get-Command** at a Windows PowerShell prompt, you will see output similar to the following:</span></span>

```
PS> Get-Command
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
Cmdlet          Add-Member                      Add-Member [-MemberType] <PS...
...
```

<span data-ttu-id="29939-106">To mnohem výstup vypadá jako výstup nápovědy Cmd.exe: tabulkový souhrn interní příkazy.</span><span class="sxs-lookup"><span data-stu-id="29939-106">This output looks a lot like the Help output of Cmd.exe: a tabular summary of internal commands.</span></span> <span data-ttu-id="29939-107">V výňatek ze **Get-Command** příkaz uvedené výše, každý příkaz zobrazí výstup má CommandType rutiny.</span><span class="sxs-lookup"><span data-stu-id="29939-107">In the excerpt of the **Get-Command** command output shown above, every command shown has a CommandType of Cmdlet.</span></span> <span data-ttu-id="29939-108">Rutiny je typ vnitřní příkazu prostředí Windows PowerShell - typ, který odpovídá zhruba na **dir** a **cd** Cmd.exe a built-ins v součásti pro UNIX, jako je například BASH příkazy.</span><span class="sxs-lookup"><span data-stu-id="29939-108">A cmdlet is Windows PowerShell's intrinsic command type - a type that corresponds roughly to the **dir** and **cd** commands of Cmd.exe and to built-ins in UNIX shells such as BASH.</span></span>

<span data-ttu-id="29939-109">Ve výstupu **Get-Command** příkaz ukončení všech definic se třemi tečkami (...) k označení, že prostředí PowerShell nemůže zobrazit celý obsah v dostupného místa.</span><span class="sxs-lookup"><span data-stu-id="29939-109">In the output of the **Get-Command** command, all the definitions end with ellipses (...) to indicate that PowerShell cannot display all the content in the available space.</span></span> <span data-ttu-id="29939-110">Když prostředí Windows PowerShell zobrazí výstup, způsobí, že výstup jako text a pak ho tak, aby data řádně nevejde se do okna uspořádá.</span><span class="sxs-lookup"><span data-stu-id="29939-110">When Windows PowerShell displays output, it formats the output as text and then arranges it to make the data fit cleanly into the window.</span></span> <span data-ttu-id="29939-111">Se věnuje to později v části na formátování.</span><span class="sxs-lookup"><span data-stu-id="29939-111">We will talk about this later in the section on formatters.</span></span>

<span data-ttu-id="29939-112">**Get-Command** rutina má **syntaxe** parametr, který získá syntaxe každou rutinu.</span><span class="sxs-lookup"><span data-stu-id="29939-112">The **Get-Command** cmdlet has a **Syntax** parameter that gets the syntax of each cmdlet.</span></span> <span data-ttu-id="29939-113">Získání syntaxe rutiny Get-Help, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="29939-113">To get the syntax of the Get-Help cmdlet, use the following command:</span></span>

<span data-ttu-id="29939-114">**Get-Help Get-Command-syntaxe**</span><span class="sxs-lookup"><span data-stu-id="29939-114">**Get-Command Get-Help -Syntax**</span></span>

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

### <a name="displaying-available-command-types"></a><span data-ttu-id="29939-115">Zobrazení dostupných příkazových typů</span><span class="sxs-lookup"><span data-stu-id="29939-115">Displaying Available Command Types</span></span>
<span data-ttu-id="29939-116">**Get-Command** příkaz nezobrazovat každý příkaz, který je k dispozici v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29939-116">The **Get-Command** command does not list every command that is available in Windows PowerShell.</span></span> <span data-ttu-id="29939-117">Místo toho **Get-Command** příkaz vypíše jenom rutiny v aktuální relaci.</span><span class="sxs-lookup"><span data-stu-id="29939-117">Instead, the **Get-Command** command lists only the cmdlets in the current session.</span></span> <span data-ttu-id="29939-118">Prostředí Windows PowerShell ve skutečnosti podporuje několik typů příkazů.</span><span class="sxs-lookup"><span data-stu-id="29939-118">Windows PowerShell actually supports several other types of commands.</span></span> <span data-ttu-id="29939-119">Aliasy, funkcí a skriptů jsou také příkazy prostředí Windows PowerShell, i když nejsou popsané v podrobností v Průvodci uživatele Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29939-119">Aliases, functions, and scripts are also Windows PowerShell commands, although they are not discussed in detail in the Windows PowerShell User's Guide.</span></span> <span data-ttu-id="29939-120">Externí soubory, které jsou spustitelné nebo obslužná rutina typ zaregistrované sdílené, jsou také klasifikovány jako příkazy.</span><span class="sxs-lookup"><span data-stu-id="29939-120">External files that are executable, or have a registered file type handler, are also classified as commands.</span></span>

<span data-ttu-id="29939-121">Chcete-li získat všechny příkazy v relaci, zadejte:</span><span class="sxs-lookup"><span data-stu-id="29939-121">To get all commands in the session, type:</span></span>

```
Get-Command *
```

<span data-ttu-id="29939-122">Tento seznam zahrnuje externí soubory v cestě vyhledávání, a proto může obsahovat tisíce položek.</span><span class="sxs-lookup"><span data-stu-id="29939-122">Because this list includes external files in your search path, it may contain thousands of items.</span></span> <span data-ttu-id="29939-123">Je více užitečné prohlédnout si omezenou sadu příkazů.</span><span class="sxs-lookup"><span data-stu-id="29939-123">It is more useful to look at a reduced set of commands.</span></span>

<span data-ttu-id="29939-124">Nativní příkazy jiné typy, použijte **CommandType** parametr **Get-Command** rutiny.</span><span class="sxs-lookup"><span data-stu-id="29939-124">To get native commands of other types, use the **CommandType** parameter of the **Get-Command** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="29939-125">Hvězdička (\*) se používá pro porovnávání v prostředí Windows PowerShell argumenty příkazu se zástupnými znaky.</span><span class="sxs-lookup"><span data-stu-id="29939-125">The asterisk (\*) is used for wildcard matching in Windows PowerShell command arguments.</span></span> <span data-ttu-id="29939-126">\* Znamená "odpovídat jeden nebo více znaky".</span><span class="sxs-lookup"><span data-stu-id="29939-126">The \* means "match one or more of any characters".</span></span> <span data-ttu-id="29939-127">Můžete zadat **Get-Command\&#42;** najít všechny příkazy, které začínají písmenem "a".</span><span class="sxs-lookup"><span data-stu-id="29939-127">You can type **Get-Command a\&#42;** to find all commands that begin with the letter "a".</span></span> <span data-ttu-id="29939-128">Na rozdíl od v Cmd.exe porovnávání se zástupnými znaky bude odpovídat zástupné prostředí Windows PowerShell taky období.</span><span class="sxs-lookup"><span data-stu-id="29939-128">Unlike wildcard matching in Cmd.exe, Windows PowerShell's wildcard will also match a period.</span></span>

<span data-ttu-id="29939-129">Chcete-li získat aliasy příkazů, které jsou přiřazené zástupné názvy příkazů, zadejte:</span><span class="sxs-lookup"><span data-stu-id="29939-129">To get command aliases, which are the assigned nicknames of commands, type:</span></span>

```
Get-Command -CommandType Alias
```

<span data-ttu-id="29939-130">Chcete-li získat funkce v aktuální relaci, zadejte:</span><span class="sxs-lookup"><span data-stu-id="29939-130">To get the functions in the current session, type:</span></span>

```
Get-Command -CommandType Function
```

<span data-ttu-id="29939-131">Chcete-li zobrazit skriptů v prostředí Windows PowerShell cesty pro hledání, zadejte:</span><span class="sxs-lookup"><span data-stu-id="29939-131">To display scripts in Windows PowerShell's search path, type:</span></span>

```
Get-Command -CommandType Script
```

