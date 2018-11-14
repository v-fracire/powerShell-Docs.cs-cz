---
ms.date: 11/13/2018
keywords: rutiny prostředí PowerShell
title: Dekódování příkazu Powershellu ze spuštěného procesu
author: randomnote1
ms.openlocfilehash: a0602070a8c5b60ce0bb09e227690f48d970a868
ms.sourcegitcommit: 91786b03704fbd2d185f674df0bc67faddfb6288
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/14/2018
ms.locfileid: "51619249"
---
# <a name="decode-a-powershell-command-from-a-running-process"></a><span data-ttu-id="ba2d4-103">Dekódování příkazu Powershellu ze spuštěného procesu</span><span class="sxs-lookup"><span data-stu-id="ba2d4-103">Decode a PowerShell command from a running process</span></span>

<span data-ttu-id="ba2d4-104">V některých případech bude pravděpodobně Powershellu je proces, který běží zabírá tak velký objem prostředků.</span><span class="sxs-lookup"><span data-stu-id="ba2d4-104">At times, you may have a PowerShell process running that is taking up a large amount of resources.</span></span>
<span data-ttu-id="ba2d4-105">Tento proces může být spuštěn v kontextu [Plánovač úloh][] úlohy nebo [Agent systému SQL Server][] úlohy.</span><span class="sxs-lookup"><span data-stu-id="ba2d4-105">This process could be running in the context of a [Task Scheduler][] job or a [SQL Server Agent][] job.</span></span> <span data-ttu-id="ba2d4-106">Pokud existuje více prostředí PowerShell procesy spuštěné, může být obtížné zjistit, který proces představuje problém.</span><span class="sxs-lookup"><span data-stu-id="ba2d4-106">Where there are multiple PowerShell processes running, it can be difficult to know which process represents the problem.</span></span> <span data-ttu-id="ba2d4-107">Tento článek popisuje, jak k dekódování blok skriptu, prostředí PowerShell proces aktuálně běží.</span><span class="sxs-lookup"><span data-stu-id="ba2d4-107">This article shows how to decode a script block that a PowerShell process is currently running.</span></span>

## <a name="create-a-long-running-process"></a><span data-ttu-id="ba2d4-108">Vytvořit dlouho běžící proces</span><span class="sxs-lookup"><span data-stu-id="ba2d4-108">Create a long running process</span></span>

<span data-ttu-id="ba2d4-109">Abychom si předvedli tento scénář, otevřete nové okno Powershellu a spusťte následující kód.</span><span class="sxs-lookup"><span data-stu-id="ba2d4-109">To demonstrate this scenario, open a new PowerShell window and run the following code.</span></span> <span data-ttu-id="ba2d4-110">Je spuštěn příkaz prostředí PowerShell, který zobrazí číslo každou minutu po dobu 10 minut.</span><span class="sxs-lookup"><span data-stu-id="ba2d4-110">It executes a PowerShell command that outputs a number every minute for 10 minutes.</span></span>

```powershell
powershell.exe -Command {
    $i = 1
    while ( $i -le 10 )
    {
        Write-Output -InputObject $i
        Start-Sleep -Seconds 60
        $i++
    }
}
```

## <a name="view-the-process"></a><span data-ttu-id="ba2d4-111">Zobrazení procesu</span><span class="sxs-lookup"><span data-stu-id="ba2d4-111">View the process</span></span>

<span data-ttu-id="ba2d4-112">Text příkazu, který provádí Powershellu je uložen v **CommandLine** vlastnost [Win32_Process][] třídy.</span><span class="sxs-lookup"><span data-stu-id="ba2d4-112">The body of the command which PowerShell is executing is stored in the **CommandLine** property of the [Win32_Process][] class.</span></span> <span data-ttu-id="ba2d4-113">Pokud je příkaz [kódovaný příkaz][], **CommandLine** vlastnost obsahuje řetězec "EncodedCommand".</span><span class="sxs-lookup"><span data-stu-id="ba2d4-113">If the command is an [encoded command][], the **CommandLine** property contains the string "EncodedCommand".</span></span> <span data-ttu-id="ba2d4-114">Na základě těchto informací může být kódovaný příkaz zrušení obfuskovaný pomocí následujícího postupu.</span><span class="sxs-lookup"><span data-stu-id="ba2d4-114">Using this information, the encoded command can be de-obfuscated via the following process.</span></span>

<span data-ttu-id="ba2d4-115">Spusťte PowerShell jako správce.</span><span class="sxs-lookup"><span data-stu-id="ba2d4-115">Start PowerShell as Administrator.</span></span> <span data-ttu-id="ba2d4-116">Je důležité, že je spuštěna prostředí PowerShell jako správce, v opačném případě se žádné výsledky při dotazování spuštěné procesy.</span><span class="sxs-lookup"><span data-stu-id="ba2d4-116">It is vital that PowerShell is running as administrator, otherwise no results are returned when querying the running processes.</span></span>

<span data-ttu-id="ba2d4-117">Spusťte následující příkaz, který získá všechny procesy prostředí PowerShell, které mají kódovaného příkaz:</span><span class="sxs-lookup"><span data-stu-id="ba2d4-117">Execute the following command to get all of the PowerShell processes that have an encoded command:</span></span>

```powershell
$powerShellProcesses = Get-CimInstance -ClassName Win32_Process -Filter 'CommandLine LIKE "%EncodedCommand%"'
```

<span data-ttu-id="ba2d4-118">Následující příkaz vytvoří vlastní objekt prostředí PowerShell, který obsahuje ID procesu a kódovaného příkazu.</span><span class="sxs-lookup"><span data-stu-id="ba2d4-118">The following command creates a custom PowerShell object that contains the process ID and the encoded command.</span></span>

```powershell
$commandDetails = $powerShellProcesses | Select-Object -Property ProcessId,
@{
    name       = 'EncodedCommand'
    expression = {
        if ( $_.CommandLine -match 'encodedCommand (.*) -inputFormat' )
        {
            return $matches[1]
        }
    }
}
```

<span data-ttu-id="ba2d4-119">Příkaz kódovaného nyní může dekódovat.</span><span class="sxs-lookup"><span data-stu-id="ba2d4-119">Now the encoded command can be decoded.</span></span> <span data-ttu-id="ba2d4-120">Následující fragment kódu Iteruje přes objekt podrobnosti příkazu dekóduje kódovaný příkazu a přidá dekódovaný příkaz zpět do objektu pro další zkoumání.</span><span class="sxs-lookup"><span data-stu-id="ba2d4-120">The following snippet iterates over the command details object, decodes the encoded command, and adds the decoded command back to the object for further investigation.</span></span>

```powershell
$commandDetails | ForEach-Object -Process {
    # Get the current process
    $currentProcess = $_

    # Convert the Base 64 string to a Byte Array
    $commandBytes = [System.Convert]::FromBase64String($currentProcess.EncodedCommand)

    # Convert the Byte Array to a string
    $decodedCommand = [System.Text.Encoding]::Unicode.GetString($commandBytes)

    # Add the decoded command back to the object
    $commandDetails |
        Where-Object -FilterScript { $_.ProcessId -eq $_.ProcessId } |
        Add-Member -MemberType NoteProperty -Name DecodedCommand -Value $decodedCommand
}
$commandDetails[0]
```

<span data-ttu-id="ba2d4-121">Dekódovaný příkazu můžete zkontrolovat nyní tak, že vyberete vlastnost dekódovaný příkazu.</span><span class="sxs-lookup"><span data-stu-id="ba2d4-121">The decoded command can now be reviewed by selecting the decoded command property.</span></span>

```output
ProcessId      : 8752
EncodedCommand : IAAKAAoACgAgAAoAIAAgACAAIAAkAGkAIAA9ACAAMQAgAAoACgAKACAACgAgACAAIAAgAHcAaABpAGwAZQAgACgAIAAkAGkAIAAtAG
                 wAZQAgADEAMAAgACkAIAAKAAoACgAgAAoAIAAgACAAIAB7ACAACgAKAAoAIAAKACAAIAAgACAAIAAgACAAIABXAHIAaQB0AGUALQBP
                 AHUAdABwAHUAdAAgAC0ASQBuAHAAdQB0AE8AYgBqAGUAYwB0ACAAJABpACAACgAKAAoAIAAKACAAIAAgACAAIAAgACAAIABTAHQAYQ
                 ByAHQALQBTAGwAZQBlAHAAIAAtAFMAZQBjAG8AbgBkAHMAIAA2ADAAIAAKAAoACgAgAAoAIAAgACAAIAAgACAAIAAgACQAaQArACsA
                 IAAKAAoACgAgAAoAIAAgACAAIAB9ACAACgAKAAoAIAAKAA==
DecodedCommand :
                     $i = 1

                     while ( $i -le 10 )

                     {

                         Write-Output -InputObject $i

                         Start-Sleep -Seconds 60

                         $i++

                     }
```

[Plánovač úloh]: /windows/desktop/TaskSchd/task-scheduler-start-page
[Task Scheduler]: /windows/desktop/TaskSchd/task-scheduler-start-page
[Agent systému SQL Server]: /sql/ssms/agent/sql-server-agent
[SQL Server Agent]: /sql/ssms/agent/sql-server-agent
[Win32_Process]: /windows/desktop/CIMWin32Prov/win32-process
[kódovaný příkaz]: /powershell/scripting/core-powershell/console/powershell.exe-command-line-help#-encodedcommand-
[encoded command]: /powershell/scripting/core-powershell/console/powershell.exe-command-line-help#-encodedcommand-
