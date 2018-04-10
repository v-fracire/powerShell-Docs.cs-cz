---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Správa procesů procesními rutinami
ms.assetid: 5038f612-d149-4698-8bbb-999986959e31
ms.openlocfilehash: d6d7daa810dce2d476566e4d30f03cc95bf730e6
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="managing-processes-with-process-cmdlets"></a><span data-ttu-id="39064-103">Správa procesů procesními rutinami</span><span class="sxs-lookup"><span data-stu-id="39064-103">Managing Processes with Process Cmdlets</span></span>

<span data-ttu-id="39064-104">Proces rutiny v prostředí Windows PowerShell můžete použít ke správě místních i vzdálených procesy v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39064-104">You can use the Process cmdlets in Windows PowerShell to manage local and remote processes in Windows PowerShell.</span></span>

## <a name="getting-processes-get-process"></a><span data-ttu-id="39064-105">Získávání procesy (Get-Process)</span><span class="sxs-lookup"><span data-stu-id="39064-105">Getting Processes (Get-Process)</span></span>

<span data-ttu-id="39064-106">Chcete-li získat procesy spuštěné v místním počítači, spusťte **Get-Process** bez parametrů.</span><span class="sxs-lookup"><span data-stu-id="39064-106">To get the processes running on the local computer, run a **Get-Process** with no parameters.</span></span>

<span data-ttu-id="39064-107">Konkrétní procesy získáte zadáním jejich procesu názvy nebo ID procesu.</span><span class="sxs-lookup"><span data-stu-id="39064-107">You can get particular processes by specifying their process names or process IDs.</span></span> <span data-ttu-id="39064-108">Následující příkaz získá nečinného procesu:</span><span class="sxs-lookup"><span data-stu-id="39064-108">The following command gets the Idle process:</span></span>

```
PS> Get-Process -id 0

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
      0       0        0         16     0               0 Idle
```

<span data-ttu-id="39064-109">I když je normální, že k rutinám, abyste vrátit žádná data v některých situacích, když zadáte proces, pomocí jeho ProcessId **Get-Process** vygeneruje chybu, pokud najde žádné shody, protože je obvykle záměr načíst známé spuštěných procesů.</span><span class="sxs-lookup"><span data-stu-id="39064-109">Although it is normal for cmdlets to return no data in some situations, when you specify a process by its ProcessId, **Get-Process** generates an error if it finds no matches, because the usual intent is to retrieve a known running process.</span></span> <span data-ttu-id="39064-110">Pokud není žádný proces s tímto Id, je pravděpodobné, že Id je nesprávné, nebo že požadovaný proces byl již ukončen:</span><span class="sxs-lookup"><span data-stu-id="39064-110">If there is no process with that Id, it is likely that the Id is incorrect or that the process of interest has already exited:</span></span>

```
PS> Get-Process -Id 99

Get-Process : No process with process ID 99 was found.
At line:1 char:12
+ Get-Process  <<<< -Id 99
```

<span data-ttu-id="39064-111">Parametr Name rutiny Get-Process můžete určit podmnožinu procesy založené na název procesu.</span><span class="sxs-lookup"><span data-stu-id="39064-111">You can use the Name parameter of the Get-Process cmdlet to specify a subset of processes based on the process name.</span></span> <span data-ttu-id="39064-112">Parametr Name, může trvat několik názvů v seznamu odděleném čárkami a podporuje použití zástupných znaků, abyste mohli zadat vzory názvů.</span><span class="sxs-lookup"><span data-stu-id="39064-112">The Name parameter can take multiple names in a comma-separated list and it supports the use of wildcards, so you can type name patterns.</span></span>

<span data-ttu-id="39064-113">Například následující příkaz získá procesu, jejichž názvy začínají řetězcem "ex."</span><span class="sxs-lookup"><span data-stu-id="39064-113">For example, the following command gets process whose names begin with "ex."</span></span>

```
PS> Get-Process -Name ex*

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    234       7     5572      12484   134     2.98   1684 EXCEL
    555      15    34500      12384   134   105.25    728 explorer
```

<span data-ttu-id="39064-114">Protože třída .NET System.Diagnostics.Process je základem pro prostředí Windows PowerShell procesy, odpovídá některé z názvů používá System.Diagnostics.Process.</span><span class="sxs-lookup"><span data-stu-id="39064-114">Because the .NET System.Diagnostics.Process class is the foundation for Windows PowerShell processes, it follows some of the conventions used by System.Diagnostics.Process.</span></span> <span data-ttu-id="39064-115">Na konci název spustitelného souboru jedním z těchto konvence je název spustitelného souboru procesu nikdy zahrnuje ".exe".</span><span class="sxs-lookup"><span data-stu-id="39064-115">One of those conventions is that the process name for an executable never includes the ".exe" at the end of the executable name.</span></span>

<span data-ttu-id="39064-116">**Get-Process** také je možné zadat více hodnot pro parametr Name.</span><span class="sxs-lookup"><span data-stu-id="39064-116">**Get-Process** also accepts multiple values for the Name parameter.</span></span>

```
PS> Get-Process -Name exp*,power*

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    540      15    35172      48148   141    88.44    408 explorer
    605       9    30668      29800   155     7.11   3052 powershell
```

<span data-ttu-id="39064-117">Parametr ComputerName Get-Process můžete získat procesy na vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="39064-117">You can use the ComputerName parameter of Get-Process to get processes on remote computers.</span></span> <span data-ttu-id="39064-118">Například následující příkaz získá procesy prostředí PowerShell v místním počítači (představované "localhost") a na dva vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="39064-118">For example, the following command gets the PowerShell processes on the local computer (represented by "localhost") and on two remote computers.</span></span>

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server02

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    258       8    29772      38636   130            3700 powershell
    398      24    75988      76800   572            5816 powershell
    605       9    30668      29800   155     7.11   3052 powershell
```

<span data-ttu-id="39064-119">Názvy počítačů nejsou v tomto zobrazení zřejmé, ale jsou uložené ve vlastnosti MachineName proces objektů, které vrátí Get-Process.</span><span class="sxs-lookup"><span data-stu-id="39064-119">The computer names are not evident in this display, but they are stored in the MachineName property of the process objects that Get-Process returns.</span></span> <span data-ttu-id="39064-120">Následující příkaz používá rutinu Format-Table pro zobrazení ID procesu, název_procesu a MachineName (ComputerName) vlastnosti objektů procesu.</span><span class="sxs-lookup"><span data-stu-id="39064-120">The following command uses the Format-Table cmdlet to display the process ID, ProcessName and MachineName (ComputerName) properties of the process objects.</span></span>

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server01 | Format-Table -Property ID, ProcessName, MachineName

  Id ProcessName MachineName
  -- ----------- -----------
3700 powershell  Server01
3052 powershell  Server02
5816 powershell  localhost
```

<span data-ttu-id="39064-121">Tento příkaz složitější přidá vlastnost MachineName standardní zobrazení Get-Process.</span><span class="sxs-lookup"><span data-stu-id="39064-121">This more complex command adds the MachineName property to the standard Get-Process display.</span></span>

```
PS> Get-Process powershell -ComputerName localhost, Server01, Server02 |
    Format-Table -Property Handles,
        @{Label="NPM(K)";Expression={[int]($_.NPM/1024)}},
        @{Label="PM(K)";Expression={[int]($_.PM/1024)}},
        @{Label="WS(K)";Expression={[int]($_.WS/1024)}},
        @{Label="VM(M)";Expression={[int]($_.VM/1MB)}},
        @{Label="CPU(s)";Expression={if ($_.CPU -ne $() {$_.CPU.ToString("N")}}},
        Id, ProcessName, MachineName -auto

Handles  NPM(K)  PM(K) WS(K) VM(M) CPU(s)  Id ProcessName  MachineName
-------  ------  ----- ----- ----- ------  -- -----------  -----------
    258       8  29772 38636   130         3700 powershell Server01
    398      24  75988 76800   572         5816 powershell localhost
    605       9  30668 29800   155 7.11    3052 powershell Server02
```

## <a name="stopping-processes-stop-process"></a><span data-ttu-id="39064-122">Zastavení procesy (Stop-Process)</span><span class="sxs-lookup"><span data-stu-id="39064-122">Stopping Processes (Stop-Process)</span></span>

<span data-ttu-id="39064-123">Prostředí Windows PowerShell poskytuje flexibilitu pro výpis procesů, ale co o zastavení procesu?</span><span class="sxs-lookup"><span data-stu-id="39064-123">Windows PowerShell gives you flexibility for listing processes, but what about stopping a process?</span></span>

<span data-ttu-id="39064-124">**Stop-Process** rutiny přebírá název nebo Id k určení chcete ukončit proces.</span><span class="sxs-lookup"><span data-stu-id="39064-124">The **Stop-Process** cmdlet takes a Name or Id to specify a process you want to stop.</span></span> <span data-ttu-id="39064-125">Možnost k zastavení procesy závisí na oprávněních.</span><span class="sxs-lookup"><span data-stu-id="39064-125">Your ability to stop processes depends on your permissions.</span></span> <span data-ttu-id="39064-126">Nelze zastavit, některé procesy.</span><span class="sxs-lookup"><span data-stu-id="39064-126">Some processes cannot be stopped.</span></span> <span data-ttu-id="39064-127">Například pokud se pokusíte zastavit nečinného procesu, dojde k chybě:</span><span class="sxs-lookup"><span data-stu-id="39064-127">For example, if you try to stop the idle process, you get an error:</span></span>

```
PS> Stop-Process -Name Idle
Stop-Process : Process 'Idle (0)' cannot be stopped due to the following error:
 Access is denied
At line:1 char:13
+ Stop-Process  <<<< -Name Idle
```

<span data-ttu-id="39064-128">Můžete taky přinutit, výzvy s **potvrdit** parametr.</span><span class="sxs-lookup"><span data-stu-id="39064-128">You can also force prompting with the **Confirm** parameter.</span></span> <span data-ttu-id="39064-129">Tento parametr je zvlášť užitečné, pokud používáte zástupný znak při zadávání názvu procesu, protože může nechtěně odpovídat některé procesy, které nechcete zastavit:</span><span class="sxs-lookup"><span data-stu-id="39064-129">This parameter is particularly useful if you use a wildcard when specifying the process name, because you may accidentally match some processes you do not want to stop:</span></span>

```
PS> Stop-Process -Name t*,e* -Confirm
Confirm
Are you sure you want to perform this action?
Performing operation "Stop-Process" on Target "explorer (408)".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):n
Confirm
Are you sure you want to perform this action?
Performing operation "Stop-Process" on Target "taskmgr (4072)".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):n
```

<span data-ttu-id="39064-130">Manipulace s složitého procesu je možné pomocí některé z objektu filtrování rutiny.</span><span class="sxs-lookup"><span data-stu-id="39064-130">Complex process manipulation is possible by using some of the object filtering cmdlets.</span></span> <span data-ttu-id="39064-131">Protože objekt procesu má odpovídá vlastnosti, která je hodnota true, pokud již není aktivní, můžete zastavit všechny neodpovídající aplikace pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="39064-131">Because a Process object has a Responding property that is true when it is no longer responding, you can stop all nonresponsive applications with the following command:</span></span>

```powershell
Get-Process | Where-Object -FilterScript {$_.Responding -eq $false} | Stop-Process
```

<span data-ttu-id="39064-132">V jiných situacích můžete použít ve stejný přístup.</span><span class="sxs-lookup"><span data-stu-id="39064-132">You can use the same approach in other situations.</span></span> <span data-ttu-id="39064-133">Předpokládejme například, že na oznámení sekundární oblasti aplikaci spustí automaticky při uživatelé začít jiná aplikace.</span><span class="sxs-lookup"><span data-stu-id="39064-133">For example, suppose a secondary notification area application automatically runs when users start another application.</span></span> <span data-ttu-id="39064-134">Můžete zjistit, že to nebude fungovat správně v relacích Terminálové služby, ale chcete zachovat v relací, které běží na konzole fyzického počítače.</span><span class="sxs-lookup"><span data-stu-id="39064-134">You may find that this does not work correctly in Terminal Services sessions, but you still want to keep it in sessions that run on the physical computer console.</span></span> <span data-ttu-id="39064-135">Relace připojení k ploše fyzického počítače vždy mít ID relace 0, tak můžete zastavit všechny instance procesu, které jsou v jiné relaci pomocí **Where-Object** a proces, **SessionId** :</span><span class="sxs-lookup"><span data-stu-id="39064-135">Sessions connected to the physical computer desktop always have a session ID of 0, so you can stop all instances of the process that are in other sessions by using **Where-Object** and the process, **SessionId**:</span></span>

```powershell
Get-Process -Name BadApp | Where-Object -FilterScript {$_.SessionId -neq 0} | Stop-Process
```

<span data-ttu-id="39064-136">Rutinu Stop-Process nemá parametr ComputerName.</span><span class="sxs-lookup"><span data-stu-id="39064-136">The Stop-Process cmdlet does not have a ComputerName parameter.</span></span> <span data-ttu-id="39064-137">Proto spustit příkaz zastavení procesu ve vzdáleném počítači, budete muset použít rutiny Invoke-Command.</span><span class="sxs-lookup"><span data-stu-id="39064-137">Therefore, to run a stop process command on a remote computer, you need to use the Invoke-Command cmdlet.</span></span> <span data-ttu-id="39064-138">Například na vzdáleném počítači Server01 zastavit proces prostředí PowerShell, zadejte:</span><span class="sxs-lookup"><span data-stu-id="39064-138">For example, to stop the PowerShell process on the Server01 remote computer, type:</span></span>

```powershell
Invoke-Command -ComputerName Server01 {Stop-Process Powershell}
```

## <a name="stopping-all-other-windows-powershell-sessions"></a><span data-ttu-id="39064-139">Zastavení všech dalších relace prostředí PowerShell systému Windows</span><span class="sxs-lookup"><span data-stu-id="39064-139">Stopping All Other Windows PowerShell Sessions</span></span>

<span data-ttu-id="39064-140">Čas od času může být užitečné mít možnost k zastavení všech spuštěných relací prostředí Windows PowerShell než aktuální relaci.</span><span class="sxs-lookup"><span data-stu-id="39064-140">It may occasionally be useful to be able to stop all running Windows PowerShell sessions other than the current session.</span></span> <span data-ttu-id="39064-141">Pokud relace používá příliš mnoho prostředků nebo je nepřístupný (ho může být spuštěn vzdáleně nebo v jiné relaci plochy), nebudete moci přímo zastavte ji.</span><span class="sxs-lookup"><span data-stu-id="39064-141">If a session is using too many resources or is inaccessible (it may be running remotely or in another desktop session), you may not be able to directly stop it.</span></span> <span data-ttu-id="39064-142">Při pokusu o zastavení všech spuštěných relací, ale aktuální relace může být ukončena místo toho.</span><span class="sxs-lookup"><span data-stu-id="39064-142">If you try to stop all running sessions, however, the current session may be terminated instead.</span></span>

<span data-ttu-id="39064-143">Každou relaci prostředí Windows PowerShell je proměnná prostředí PID, který obsahuje Id procesu prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39064-143">Each Windows PowerShell session has an environment variable PID that contains the Id of the Windows PowerShell process.</span></span> <span data-ttu-id="39064-144">Můžete zkontrolovat $PID proti Id každé relaci a ukončit pouze relace prostředí Windows PowerShell, které mají jiné ID. Následující příkaz kanálu tuto akci provede a vrátí seznam ukončenou relací (protože se používá **PassThru** parametr):</span><span class="sxs-lookup"><span data-stu-id="39064-144">You can check the $PID against the Id of each session and terminate only Windows PowerShell sessions that have a different Id. The following pipeline command does this and returns the list of terminated sessions (because of the use of the **PassThru** parameter):</span></span>

```
PS> Get-Process -Name powershell | Where-Object -FilterScript {$_.Id -ne $PID} | Stop-Process -PassThru

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    334       9    23348      29136   143     1.03    388 powershell
    304       9    23152      29040   143     1.03    632 powershell
    302       9    20916      26804   143     1.03   1116 powershell
    335       9    25656      31412   143     1.09   3452 powershell
    303       9    23156      29044   143     1.05   3608 powershell
    287       9    21044      26928   143     1.02   3672 powershell
```

## <a name="starting-debugging-and-waiting-for-processes"></a><span data-ttu-id="39064-145">Spuštění, ladění a čeká na procesy</span><span class="sxs-lookup"><span data-stu-id="39064-145">Starting, Debugging, and Waiting for Processes</span></span>

<span data-ttu-id="39064-146">Prostředí Windows PowerShell taky obsahuje rutiny start (nebo restartování), ladění proces a počkejte na dokončení před spuštěním příkazu procesu.</span><span class="sxs-lookup"><span data-stu-id="39064-146">Windows PowerShell also comes with cmdlets to start (or restart), debug a process, and wait for a process to complete before running a command.</span></span> <span data-ttu-id="39064-147">Informace o těchto rutinách najdete v tématu nápovědy rutiny pro všechny rutiny.</span><span class="sxs-lookup"><span data-stu-id="39064-147">For information about these cmdlets, see the cmdlet help topic for each cmdlet.</span></span>

## <a name="see-also"></a><span data-ttu-id="39064-148">Viz také</span><span class="sxs-lookup"><span data-stu-id="39064-148">See Also</span></span>

- <span data-ttu-id="39064-149">[Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)</span><span class="sxs-lookup"><span data-stu-id="39064-149">[Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)</span></span>
- <span data-ttu-id="39064-150">[Stop-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)</span><span class="sxs-lookup"><span data-stu-id="39064-150">[Stop-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)</span></span>
- [<span data-ttu-id="39064-151">Proces spuštění</span><span class="sxs-lookup"><span data-stu-id="39064-151">Start-Process</span></span>](https://technet.microsoft.com/en-us/library/41a7e43c-9bb3-4dc2-8b0c-f6c32962e72c)
- [<span data-ttu-id="39064-152">Wait-Process</span><span class="sxs-lookup"><span data-stu-id="39064-152">Wait-Process</span></span>](https://technet.microsoft.com/en-us/library/9222af7a-789d-4a09-aa90-09d7c256c799)
- [<span data-ttu-id="39064-153">Ladění procesu</span><span class="sxs-lookup"><span data-stu-id="39064-153">Debug-Process</span></span>](https://technet.microsoft.com/en-us/library/eea1dace-3913-4dbd-b659-5a94a610eee1)
- [<span data-ttu-id="39064-154">Invoke-Command</span><span class="sxs-lookup"><span data-stu-id="39064-154">Invoke-Command</span></span>](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)