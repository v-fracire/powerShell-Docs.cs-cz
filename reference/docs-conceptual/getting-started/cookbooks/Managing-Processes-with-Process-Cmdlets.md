---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Správa procesů pomocí rutiny procesu"
ms.assetid: 5038f612-d149-4698-8bbb-999986959e31
ms.openlocfilehash: 3786fb77167746d6a477dffdd4ea13e863c99964
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="managing-processes-with-process-cmdlets"></a>Správa procesů pomocí rutiny procesu
Proces rutiny v prostředí Windows PowerShell můžete použít ke správě místních i vzdálených procesy v prostředí Windows PowerShell.

## <a name="getting-processes-get-process"></a>Získávání procesy (Get-Process)
Chcete-li získat procesy spuštěné v místním počítači, spusťte **Get-Process** bez parametrů.

Konkrétní procesy získáte zadáním jejich procesu názvy nebo ID procesu. Následující příkaz získá nečinného procesu:

```
PS> Get-Process -id 0
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
      0       0        0         16     0               0 Idle
```

I když je normální, že k rutinám, abyste vrátit žádná data v některých situacích, když zadáte proces, pomocí jeho ProcessId **Get-Process** vygeneruje chybu, pokud najde žádné shody, protože je obvykle záměr načíst známé spuštěných procesů. Pokud není žádný proces s tímto Id, je pravděpodobné, že Id je nesprávné, nebo že požadovaný proces byl již ukončen:

```
PS> Get-Process -Id 99
Get-Process : No process with process ID 99 was found.
At line:1 char:12
+ Get-Process  <<<< -Id 99
```

Parametr Name rutiny Get-Process můžete určit podmnožinu procesy založené na název procesu. Parametr Name, může trvat několik názvů v seznamu odděleném čárkami a podporuje použití zástupných znaků, abyste mohli zadat vzory názvů.

Například následující příkaz získá procesu, jejichž názvy začínají řetězcem "ex."

```
PS> Get-Process -Name ex*
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    234       7     5572      12484   134     2.98   1684 EXCEL
    555      15    34500      12384   134   105.25    728 explorer
```

Protože třída .NET System.Diagnostics.Process je základem pro prostředí Windows PowerShell procesy, odpovídá některé z názvů používá System.Diagnostics.Process. Na konci název spustitelného souboru jedním z těchto konvence je název spustitelného souboru procesu nikdy zahrnuje ".exe".

**Get-Process** také je možné zadat více hodnot pro parametr Name.

```
PS> Get-Process -Name exp*,power* 
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    540      15    35172      48148   141    88.44    408 explorer
    605       9    30668      29800   155     7.11   3052 powershell
```

Parametr ComputerName Get-Process můžete získat procesy na vzdálených počítačích. Například následující příkaz získá procesy prostředí PowerShell v místním počítači (představované "localhost") a na dva vzdálených počítačích.

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server02
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    258       8    29772      38636   130            3700 powershell
    398      24    75988      76800   572            5816 powershell
    605       9    30668      29800   155     7.11   3052 powershell
```

Názvy počítačů nejsou v tomto zobrazení zřejmé, ale jsou uložené ve vlastnosti MachineName proces objektů, které vrátí Get-Process. Následující příkaz používá rutinu Format-Table pro zobrazení ID procesu, název_procesu a MachineName (ComputerName) vlastnosti objektů procesu.

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server01 | Format-Table -Property ID, ProcessName, MachineName
  Id ProcessName MachineName
  -- ----------- -----------
3700 powershell  Server01
3052 powershell  Server02
5816 powershell  localhost
```

Tento příkaz složitější přidá vlastnost MachineName standardní zobrazení Get-Process. Backtick (\`)(ASCII 96) je znak pro pokračování prostředí Windows PowerShell.

```
get-process powershell -computername localhost, Server01, Server02 | format-table -property Handles, `
                    @{Label="NPM(K)";Expression={[int]($_.NPM/1024)}}, `
                    @{Label="PM(K)";Expression={[int]($_.PM/1024)}}, `
                    @{Label="WS(K)";Expression={[int]($_.WS/1024)}}, `
                    @{Label="VM(M)";Expression={[int]($_.VM/1MB)}}, `
                    @{Label="CPU(s)";Expression={if ($_.CPU -ne $()` 
                    {$_.CPU.ToString("N")}}}, `                                                                         
                    Id, ProcessName, MachineName -auto

Handles  NPM(K)  PM(K) WS(K) VM(M) CPU(s)  Id ProcessName  MachineName
-------  ------  ----- ----- ----- ------  -- -----------  -----------
    258       8  29772 38636   130         3700 powershell Server01
    398      24  75988 76800   572         5816 powershell localhost
    605       9  30668 29800   155 7.11    3052 powershell Server02
```

## <a name="stopping-processes-stop-process"></a>Zastavení procesy (Stop-Process)
Prostředí Windows PowerShell poskytuje flexibilitu pro výpis procesů, ale co o zastavení procesu?

**Stop-Process** rutiny přebírá název nebo Id k určení chcete ukončit proces. Možnost k zastavení procesy závisí na oprávněních. Nelze zastavit, některé procesy. Například pokud se pokusíte zastavit nečinného procesu, dojde k chybě:

```
PS> Stop-Process -Name Idle
Stop-Process : Process 'Idle (0)' cannot be stopped due to the following error:
 Access is denied
At line:1 char:13
+ Stop-Process  <<<< -Name Idle
```

Můžete taky přinutit, výzvy s **potvrdit** parametr. Tento parametr je zvlášť užitečné, pokud používáte zástupný znak při zadávání názvu procesu, protože může nechtěně odpovídat některé procesy, které nechcete zastavit:

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

Manipulace s složitého procesu je možné pomocí některé z objektu filtrování rutiny. Protože objekt procesu má odpovídá vlastnosti, která je hodnota true, pokud již není aktivní, můžete zastavit všechny neodpovídající aplikace pomocí následujícího příkazu:

```
Get-Process | Where-Object -FilterScript {$_.Responding -eq $false} | Stop-Process
```

V jiných situacích můžete použít ve stejný přístup. Předpokládejme například, že na oznámení sekundární oblasti aplikaci spustí automaticky při uživatelé začít jiná aplikace. Můžete zjistit, že to nebude fungovat správně v relacích Terminálové služby, ale chcete zachovat v relací, které běží na konzole fyzického počítače. Relace připojení k ploše fyzického počítače vždy mít ID relace 0, tak můžete zastavit všechny instance procesu, které jsou v jiné relaci pomocí **Where-Object** a proces, **SessionId** :

```
Get-Process -Name BadApp | Where-Object -FilterScript {$_.SessionId -neq 0} | Stop-Process
```

Rutinu Stop-Process nemá parametr ComputerName. Proto spustit příkaz zastavení procesu ve vzdáleném počítači, budete muset použít rutiny Invoke-Command. Například na vzdáleném počítači Server01 zastavit proces prostředí PowerShell, zadejte:

```
Invoke-Command -ComputerName Server01 {Stop-Process Powershell}
```

## <a name="stopping-all-other-windows-powershell-sessions"></a>Zastavení všech dalších relace prostředí PowerShell systému Windows
Čas od času může být užitečné mít možnost k zastavení všech spuštěných relací prostředí Windows PowerShell než aktuální relaci. Pokud relace používá příliš mnoho prostředků nebo je nepřístupný (ho může být spuštěn vzdáleně nebo v jiné relaci plochy), nebudete moci přímo zastavte ji. Při pokusu o zastavení všech spuštěných relací, ale aktuální relace může být ukončena místo toho.

Každou relaci prostředí Windows PowerShell je proměnná prostředí PID, který obsahuje Id procesu prostředí Windows PowerShell. Můžete zkontrolovat $PID proti Id každé relaci a ukončit pouze relace prostředí Windows PowerShell, které mají jiné ID. Následující příkaz kanálu tuto akci provede a vrátí seznam ukončenou relací (protože se používá **PassThru** parametr):

```
PS> Get-Process -Name powershell | Where-Object -FilterScript {$_.Id -ne $PID} | Stop-Process -
PassThru
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    334       9    23348      29136   143     1.03    388 powershell
    304       9    23152      29040   143     1.03    632 powershell
    302       9    20916      26804   143     1.03   1116 powershell
    335       9    25656      31412   143     1.09   3452 powershell
    303       9    23156      29044   143     1.05   3608 powershell
    287       9    21044      26928   143     1.02   3672 powershell
```

## <a name="starting-debugging-and-waiting-for-processes"></a>Spuštění, ladění a čeká na procesy
Prostředí Windows PowerShell taky obsahuje rutiny start (nebo restartování), ladění proces a počkejte na dokončení před spuštěním příkazu procesu. Informace o těchto rutinách najdete v tématu nápovědy rutiny pro všechny rutiny.

## <a name="see-also"></a>Viz také
- [Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)
- [Stop-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)
- [Proces spuštění](https://technet.microsoft.com/en-us/library/41a7e43c-9bb3-4dc2-8b0c-f6c32962e72c)
- [Proces čekání](https://technet.microsoft.com/en-us/library/9222af7a-789d-4a09-aa90-09d7c256c799)
- [Ladění procesu](https://technet.microsoft.com/en-us/library/eea1dace-3913-4dbd-b659-5a94a610eee1)
- [Invoke-Command](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)

