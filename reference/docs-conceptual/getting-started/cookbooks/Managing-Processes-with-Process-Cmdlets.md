---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Správa procesů procesními rutinami
ms.assetid: 5038f612-d149-4698-8bbb-999986959e31
ms.openlocfilehash: 741a3464bce6284c4933384398c4e9ddcca2572c
ms.sourcegitcommit: 417b5a40cde51029de9ed8e005732978d92c9057
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2018
ms.locfileid: "46013137"
---
# <a name="managing-processes-with-process-cmdlets"></a><span data-ttu-id="ae41f-103">Správa procesů procesními rutinami</span><span class="sxs-lookup"><span data-stu-id="ae41f-103">Managing Processes with Process Cmdlets</span></span>

<span data-ttu-id="ae41f-104">Procesními rutinami ve Windows Powershellu můžete použít ke správě místních i vzdálených procesů v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ae41f-104">You can use the Process cmdlets in Windows PowerShell to manage local and remote processes in Windows PowerShell.</span></span>

## <a name="getting-processes-get-process"></a><span data-ttu-id="ae41f-105">Získávají se procesy (Get-Process)</span><span class="sxs-lookup"><span data-stu-id="ae41f-105">Getting Processes (Get-Process)</span></span>

<span data-ttu-id="ae41f-106">Chcete-li získat procesy spuštěné v místním počítači, spusťte **Get-Process** bez parametrů.</span><span class="sxs-lookup"><span data-stu-id="ae41f-106">To get the processes running on the local computer, run a **Get-Process** with no parameters.</span></span>

<span data-ttu-id="ae41f-107">Zadáním jejich názvy procesů nebo ID můžete získat konkrétní procesy.</span><span class="sxs-lookup"><span data-stu-id="ae41f-107">You can get particular processes by specifying their process names or process IDs.</span></span> <span data-ttu-id="ae41f-108">V následujícím příkazu je získán nečinného procesu:</span><span class="sxs-lookup"><span data-stu-id="ae41f-108">The following command gets the Idle process:</span></span>

```
PS> Get-Process -id 0

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
      0       0        0         16     0               0 Idle
```

<span data-ttu-id="ae41f-109">I když je běžné, že rutiny, které nevracejí žádná data v některých případech, když zadáte proces, při jeho ProcessId **Get-Process** vygeneruje chybu, pokud najde žádné shody, protože obvykle záměrem je načíst známé spuštěnému procesu.</span><span class="sxs-lookup"><span data-stu-id="ae41f-109">Although it is normal for cmdlets to return no data in some situations, when you specify a process by its ProcessId, **Get-Process** generates an error if it finds no matches, because the usual intent is to retrieve a known running process.</span></span> <span data-ttu-id="ae41f-110">Pokud neexistuje žádný proces s tímto Id, je pravděpodobné, že Id je nesprávný nebo proces byl již ukončen:</span><span class="sxs-lookup"><span data-stu-id="ae41f-110">If there is no process with that Id, it is likely that the Id is incorrect or that the process of interest has already exited:</span></span>

```
PS> Get-Process -Id 99

Get-Process : No process with process ID 99 was found.
At line:1 char:12
+ Get-Process  <<<< -Id 99
```

<span data-ttu-id="ae41f-111">Parametru Name rutiny Get-Process můžete použít k určení podmnožiny procesů podle názvu procesu.</span><span class="sxs-lookup"><span data-stu-id="ae41f-111">You can use the Name parameter of the Get-Process cmdlet to specify a subset of processes based on the process name.</span></span> <span data-ttu-id="ae41f-112">Parametr Name může trvat několik názvů v seznamu odděleném čárkami a podporuje použití zástupných znaků, takže můžete zadat název vzorce.</span><span class="sxs-lookup"><span data-stu-id="ae41f-112">The Name parameter can take multiple names in a comma-separated list and it supports the use of wildcards, so you can type name patterns.</span></span>

<span data-ttu-id="ae41f-113">Například v následujícím příkazu je získán procesu, jejichž názvy začínají řetězcem "např."</span><span class="sxs-lookup"><span data-stu-id="ae41f-113">For example, the following command gets process whose names begin with "ex."</span></span>

```
PS> Get-Process -Name ex*

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    234       7     5572      12484   134     2.98   1684 EXCEL
    555      15    34500      12384   134   105.25    728 explorer
```

<span data-ttu-id="ae41f-114">Protože třída .NET System.Diagnostics.Process je základem pro prostředí Windows PowerShell procesy, následuje některé konvence používají System.Diagnostics.Process.</span><span class="sxs-lookup"><span data-stu-id="ae41f-114">Because the .NET System.Diagnostics.Process class is the foundation for Windows PowerShell processes, it follows some of the conventions used by System.Diagnostics.Process.</span></span> <span data-ttu-id="ae41f-115">Na konci názvu spustitelného souboru jedním z těchto konvence je, že název procesu pro spustitelný soubor nikdy obsahuje ".exe".</span><span class="sxs-lookup"><span data-stu-id="ae41f-115">One of those conventions is that the process name for an executable never includes the ".exe" at the end of the executable name.</span></span>

<span data-ttu-id="ae41f-116">**Get-Process** také přijímá více hodnot pro parametr Name.</span><span class="sxs-lookup"><span data-stu-id="ae41f-116">**Get-Process** also accepts multiple values for the Name parameter.</span></span>

```
PS> Get-Process -Name exp*,power*

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    540      15    35172      48148   141    88.44    408 explorer
    605       9    30668      29800   155     7.11   3052 powershell
```

<span data-ttu-id="ae41f-117">Parametr ComputerName Get-Process můžete načíst procesy na vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="ae41f-117">You can use the ComputerName parameter of Get-Process to get processes on remote computers.</span></span> <span data-ttu-id="ae41f-118">Například následující příkaz získá postupy Powershellu v místním počítači (reprezentovaný identifikátorem "localhost") a na dvě vzdálené počítače.</span><span class="sxs-lookup"><span data-stu-id="ae41f-118">For example, the following command gets the PowerShell processes on the local computer (represented by "localhost") and on two remote computers.</span></span>

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server02

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    258       8    29772      38636   130            3700 powershell
    398      24    75988      76800   572            5816 powershell
    605       9    30668      29800   155     7.11   3052 powershell
```

<span data-ttu-id="ae41f-119">Názvy počítačů nejsou v tomto zobrazení zřejmé, ale jsou uložená ve vlastnosti MachineName procesu objektů, které vrátí Get-Process.</span><span class="sxs-lookup"><span data-stu-id="ae41f-119">The computer names are not evident in this display, but they are stored in the MachineName property of the process objects that Get-Process returns.</span></span> <span data-ttu-id="ae41f-120">Následující příkaz používá rutinu Format-Table k zobrazení ID procesu, ProcessName a MachineName (ComputerName) vlastnosti objektů process.</span><span class="sxs-lookup"><span data-stu-id="ae41f-120">The following command uses the Format-Table cmdlet to display the process ID, ProcessName and MachineName (ComputerName) properties of the process objects.</span></span>

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server01 | Format-Table -Property ID, ProcessName, MachineName

  Id ProcessName MachineName
  -- ----------- -----------
3700 powershell  Server01
3052 powershell  Server02
5816 powershell  localhost
```

<span data-ttu-id="ae41f-121">Složitější příkaz přidá vlastnost MachineName standardní zobrazení Get-Process.</span><span class="sxs-lookup"><span data-stu-id="ae41f-121">This more complex command adds the MachineName property to the standard Get-Process display.</span></span>

```
PS> Get-Process powershell -ComputerName localhost, Server01, Server02 |
    Format-Table -Property Handles,
        @{Label="NPM(K)";Expression={[int]($_.NPM/1024)}},
        @{Label="PM(K)";Expression={[int]($_.PM/1024)}},
        @{Label="WS(K)";Expression={[int]($_.WS/1024)}},
        @{Label="VM(M)";Expression={[int]($_.VM/1MB)}},
        @{Label="CPU(s)";Expression={if ($_.CPU -ne $()){$_.CPU.ToString("N")}}},
        Id, ProcessName, MachineName -auto

Handles  NPM(K)  PM(K) WS(K) VM(M) CPU(s)  Id ProcessName  MachineName
-------  ------  ----- ----- ----- ------  -- -----------  -----------
    258       8  29772 38636   130         3700 powershell Server01
    398      24  75988 76800   572         5816 powershell localhost
    605       9  30668 29800   155 7.11    3052 powershell Server02
```

## <a name="stopping-processes-stop-process"></a><span data-ttu-id="ae41f-122">Zastavuje se procesy (zastavit proces)</span><span class="sxs-lookup"><span data-stu-id="ae41f-122">Stopping Processes (Stop-Process)</span></span>

<span data-ttu-id="ae41f-123">Prostředí Windows PowerShell poskytuje flexibilitu pro výpis procesů, ale co zastavení procesu?</span><span class="sxs-lookup"><span data-stu-id="ae41f-123">Windows PowerShell gives you flexibility for listing processes, but what about stopping a process?</span></span>

<span data-ttu-id="ae41f-124">**Stop-Process** rutina použije název nebo Id k určení procesu chcete zastavit.</span><span class="sxs-lookup"><span data-stu-id="ae41f-124">The **Stop-Process** cmdlet takes a Name or Id to specify a process you want to stop.</span></span> <span data-ttu-id="ae41f-125">Možnost ukončit procesy závisí na vašich oprávněních.</span><span class="sxs-lookup"><span data-stu-id="ae41f-125">Your ability to stop processes depends on your permissions.</span></span> <span data-ttu-id="ae41f-126">Nelze zastavit, některé procesy.</span><span class="sxs-lookup"><span data-stu-id="ae41f-126">Some processes cannot be stopped.</span></span> <span data-ttu-id="ae41f-127">Například pokud se pokusíte zastavte sledovací proces nečinné, dojde k chybě:</span><span class="sxs-lookup"><span data-stu-id="ae41f-127">For example, if you try to stop the idle process, you get an error:</span></span>

```
PS> Stop-Process -Name Idle
Stop-Process : Process 'Idle (0)' cannot be stopped due to the following error:
 Access is denied
At line:1 char:13
+ Stop-Process  <<<< -Name Idle
```

<span data-ttu-id="ae41f-128">Můžete také vynutit dotazování se **potvrdit** parametru.</span><span class="sxs-lookup"><span data-stu-id="ae41f-128">You can also force prompting with the **Confirm** parameter.</span></span> <span data-ttu-id="ae41f-129">Tento parametr je zvlášť užitečné, pokud používáte zástupný znak při zadávání názvu procesu, protože může nechtěně odpovídá některé procesy, které nechcete zastavit:</span><span class="sxs-lookup"><span data-stu-id="ae41f-129">This parameter is particularly useful if you use a wildcard when specifying the process name, because you may accidentally match some processes you do not want to stop:</span></span>

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

<span data-ttu-id="ae41f-130">Pomocí některé z filtrování rutiny objektu je možné manipulaci s složitý proces.</span><span class="sxs-lookup"><span data-stu-id="ae41f-130">Complex process manipulation is possible by using some of the object filtering cmdlets.</span></span> <span data-ttu-id="ae41f-131">Protože objekt procesu má odpovídá vlastnost, která má hodnotu true, pokud již není aktivní, můžete zastavit všechny neodpovídající aplikace pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="ae41f-131">Because a Process object has a Responding property that is true when it is no longer responding, you can stop all nonresponsive applications with the following command:</span></span>

```powershell
Get-Process | Where-Object -FilterScript {$_.Responding -eq $false} | Stop-Process
```

<span data-ttu-id="ae41f-132">Stejný přístup můžete použít v jiných situacích.</span><span class="sxs-lookup"><span data-stu-id="ae41f-132">You can use the same approach in other situations.</span></span> <span data-ttu-id="ae41f-133">Předpokládejme například, že aplikace sekundární oznamovací oblasti automaticky spustí, když uživatel spustí jinou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="ae41f-133">For example, suppose a secondary notification area application automatically runs when users start another application.</span></span> <span data-ttu-id="ae41f-134">Může se stát, že to nebude fungovat správně v relací Terminálové služby, ale chcete zachovat v relacích, které běží na konzole fyzického počítače.</span><span class="sxs-lookup"><span data-stu-id="ae41f-134">You may find that this does not work correctly in Terminal Services sessions, but you still want to keep it in sessions that run on the physical computer console.</span></span> <span data-ttu-id="ae41f-135">Relace připojení k desktopu fyzického počítače vždy mít ID relace 0, tak můžete zastavit všechny instance procesu, které jsou v jiných relacích pomocí **Where-Object** a procesu **SessionId** :</span><span class="sxs-lookup"><span data-stu-id="ae41f-135">Sessions connected to the physical computer desktop always have a session ID of 0, so you can stop all instances of the process that are in other sessions by using **Where-Object** and the process, **SessionId**:</span></span>

```powershell
Get-Process -Name BadApp | Where-Object -FilterScript {$_.SessionId -neq 0} | Stop-Process
```

<span data-ttu-id="ae41f-136">Rutinu Stop-Process nemá parametr ComputerName.</span><span class="sxs-lookup"><span data-stu-id="ae41f-136">The Stop-Process cmdlet does not have a ComputerName parameter.</span></span> <span data-ttu-id="ae41f-137">Proto se ke spuštění příkazu stop procesu ve vzdáleném počítači, budete muset použít rutiny Invoke-Command.</span><span class="sxs-lookup"><span data-stu-id="ae41f-137">Therefore, to run a stop process command on a remote computer, you need to use the Invoke-Command cmdlet.</span></span> <span data-ttu-id="ae41f-138">Na vzdáleném počítači Server01 zastavte sledovací proces prostředí PowerShell, zadejte například:</span><span class="sxs-lookup"><span data-stu-id="ae41f-138">For example, to stop the PowerShell process on the Server01 remote computer, type:</span></span>

```powershell
Invoke-Command -ComputerName Server01 {Stop-Process Powershell}
```

## <a name="stopping-all-other-windows-powershell-sessions"></a><span data-ttu-id="ae41f-139">Zastavuje se všechny ostatní relace Windows Powershellu</span><span class="sxs-lookup"><span data-stu-id="ae41f-139">Stopping All Other Windows PowerShell Sessions</span></span>

<span data-ttu-id="ae41f-140">Čas od času může být užitečné umožnit zastavit všechny spuštěné relace Windows Powershellu než aktuální relaci.</span><span class="sxs-lookup"><span data-stu-id="ae41f-140">It may occasionally be useful to be able to stop all running Windows PowerShell sessions other than the current session.</span></span> <span data-ttu-id="ae41f-141">Pokud relace využívá příliš mnoho prostředků, nebo je nepřístupný (to však mohou používat vzdáleně, nebo v jiné relaci plochy), nebudete moci přímo zastavit.</span><span class="sxs-lookup"><span data-stu-id="ae41f-141">If a session is using too many resources or is inaccessible (it may be running remotely or in another desktop session), you may not be able to directly stop it.</span></span> <span data-ttu-id="ae41f-142">Při pokusu o zastavení všech spuštěných relací, ale aktuální relaci, mohou skončit.</span><span class="sxs-lookup"><span data-stu-id="ae41f-142">If you try to stop all running sessions, however, the current session may be terminated instead.</span></span>

<span data-ttu-id="ae41f-143">Každé relaci prostředí Windows PowerShell obsahuje proměnné prostředí PID, který obsahuje Id procesu prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ae41f-143">Each Windows PowerShell session has an environment variable PID that contains the Id of the Windows PowerShell process.</span></span> <span data-ttu-id="ae41f-144">Můžete zkontrolovat $PID pro Id každé relaci a ukončí pouze relace Windows Powershellu, které mají jiné Id. Pomocí následujícího příkazu kanál to dělá a vrátí seznam ukončení relace (protože se používá **PassThru** parametr):</span><span class="sxs-lookup"><span data-stu-id="ae41f-144">You can check the $PID against the Id of each session and terminate only Windows PowerShell sessions that have a different Id. The following pipeline command does this and returns the list of terminated sessions (because of the use of the **PassThru** parameter):</span></span>

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

## <a name="starting-debugging-and-waiting-for-processes"></a><span data-ttu-id="ae41f-145">Spuštění, ladění a čekání na procesy</span><span class="sxs-lookup"><span data-stu-id="ae41f-145">Starting, Debugging, and Waiting for Processes</span></span>

<span data-ttu-id="ae41f-146">Prostředí Windows PowerShell taky obsahuje rutiny start (nebo restartování), ladicí proces a počkejte na dokončení před spuštěním příkazu procesu.</span><span class="sxs-lookup"><span data-stu-id="ae41f-146">Windows PowerShell also comes with cmdlets to start (or restart), debug a process, and wait for a process to complete before running a command.</span></span> <span data-ttu-id="ae41f-147">Informace o těchto rutinách najdete v tématu nápovědy rutiny pro každou rutinu.</span><span class="sxs-lookup"><span data-stu-id="ae41f-147">For information about these cmdlets, see the cmdlet help topic for each cmdlet.</span></span>

## <a name="see-also"></a><span data-ttu-id="ae41f-148">Viz také</span><span class="sxs-lookup"><span data-stu-id="ae41f-148">See Also</span></span>

- <span data-ttu-id="ae41f-149">[Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)</span><span class="sxs-lookup"><span data-stu-id="ae41f-149">[Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)</span></span>
- <span data-ttu-id="ae41f-150">[Stop-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)</span><span class="sxs-lookup"><span data-stu-id="ae41f-150">[Stop-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)</span></span>
- [<span data-ttu-id="ae41f-151">Spustit proces</span><span class="sxs-lookup"><span data-stu-id="ae41f-151">Start-Process</span></span>](https://technet.microsoft.com/en-us/library/41a7e43c-9bb3-4dc2-8b0c-f6c32962e72c)
- [<span data-ttu-id="ae41f-152">Wait – proces</span><span class="sxs-lookup"><span data-stu-id="ae41f-152">Wait-Process</span></span>](https://technet.microsoft.com/en-us/library/9222af7a-789d-4a09-aa90-09d7c256c799)
- [<span data-ttu-id="ae41f-153">Proces ladění</span><span class="sxs-lookup"><span data-stu-id="ae41f-153">Debug-Process</span></span>](https://technet.microsoft.com/en-us/library/eea1dace-3913-4dbd-b659-5a94a610eee1)
- [<span data-ttu-id="ae41f-154">Invoke-Command</span><span class="sxs-lookup"><span data-stu-id="ae41f-154">Invoke-Command</span></span>](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)
