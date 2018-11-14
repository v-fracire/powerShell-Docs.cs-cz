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
# <a name="decode-a-powershell-command-from-a-running-process"></a>Dekódování příkazu Powershellu ze spuštěného procesu

V některých případech bude pravděpodobně Powershellu je proces, který běží zabírá tak velký objem prostředků.
Tento proces může být spuštěn v kontextu [Plánovač úloh][] úlohy nebo [Agent systému SQL Server][] úlohy. Pokud existuje více prostředí PowerShell procesy spuštěné, může být obtížné zjistit, který proces představuje problém. Tento článek popisuje, jak k dekódování blok skriptu, prostředí PowerShell proces aktuálně běží.

## <a name="create-a-long-running-process"></a>Vytvořit dlouho běžící proces

Abychom si předvedli tento scénář, otevřete nové okno Powershellu a spusťte následující kód. Je spuštěn příkaz prostředí PowerShell, který zobrazí číslo každou minutu po dobu 10 minut.

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

## <a name="view-the-process"></a>Zobrazení procesu

Text příkazu, který provádí Powershellu je uložen v **CommandLine** vlastnost [Win32_Process][] třídy. Pokud je příkaz [kódovaný příkaz][], **CommandLine** vlastnost obsahuje řetězec "EncodedCommand". Na základě těchto informací může být kódovaný příkaz zrušení obfuskovaný pomocí následujícího postupu.

Spusťte PowerShell jako správce. Je důležité, že je spuštěna prostředí PowerShell jako správce, v opačném případě se žádné výsledky při dotazování spuštěné procesy.

Spusťte následující příkaz, který získá všechny procesy prostředí PowerShell, které mají kódovaného příkaz:

```powershell
$powerShellProcesses = Get-CimInstance -ClassName Win32_Process -Filter 'CommandLine LIKE "%EncodedCommand%"'
```

Následující příkaz vytvoří vlastní objekt prostředí PowerShell, který obsahuje ID procesu a kódovaného příkazu.

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

Příkaz kódovaného nyní může dekódovat. Následující fragment kódu Iteruje přes objekt podrobnosti příkazu dekóduje kódovaný příkazu a přidá dekódovaný příkaz zpět do objektu pro další zkoumání.

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

Dekódovaný příkazu můžete zkontrolovat nyní tak, že vyberete vlastnost dekódovaný příkazu.

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
[Agent systému SQL Server]: /sql/ssms/agent/sql-server-agent
[Win32_Process]: /windows/desktop/CIMWin32Prov/win32-process
[kódovaný příkaz]: /powershell/scripting/core-powershell/console/powershell.exe-command-line-help#-encodedcommand-
