---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Správa procesů procesními rutinami
ms.assetid: 5038f612-d149-4698-8bbb-999986959e31
ms.openlocfilehash: 741a3464bce6284c4933384398c4e9ddcca2572c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403647"
---
# <a name="managing-processes-with-process-cmdlets"></a>Správa procesů procesními rutinami

Procesními rutinami ve Windows Powershellu můžete použít ke správě místních i vzdálených procesů v prostředí Windows PowerShell.

## <a name="getting-processes-get-process"></a>Získávají se procesy (Get-Process)

Chcete-li získat procesy spuštěné v místním počítači, spusťte **Get-Process** bez parametrů.

Zadáním jejich názvy procesů nebo ID můžete získat konkrétní procesy. V následujícím příkazu je získán nečinného procesu:

```
PS> Get-Process -id 0

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
      0       0        0         16     0               0 Idle
```

I když je běžné, že rutiny, které nevracejí žádná data v některých případech, když zadáte proces, při jeho ProcessId **Get-Process** vygeneruje chybu, pokud najde žádné shody, protože obvykle záměrem je načíst známé spuštěnému procesu. Pokud neexistuje žádný proces s tímto Id, je pravděpodobné, že Id je nesprávný nebo proces byl již ukončen:

```
PS> Get-Process -Id 99

Get-Process : No process with process ID 99 was found.
At line:1 char:12
+ Get-Process  <<<< -Id 99
```

Parametru Name rutiny Get-Process můžete použít k určení podmnožiny procesů podle názvu procesu. Parametr Name může trvat několik názvů v seznamu odděleném čárkami a podporuje použití zástupných znaků, takže můžete zadat název vzorce.

Například v následujícím příkazu je získán procesu, jejichž názvy začínají řetězcem "např."

```
PS> Get-Process -Name ex*

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    234       7     5572      12484   134     2.98   1684 EXCEL
    555      15    34500      12384   134   105.25    728 explorer
```

Protože třída .NET System.Diagnostics.Process je základem pro prostředí Windows PowerShell procesy, následuje některé konvence používají System.Diagnostics.Process. Na konci názvu spustitelného souboru jedním z těchto konvence je, že název procesu pro spustitelný soubor nikdy obsahuje ".exe".

**Get-Process** také přijímá více hodnot pro parametr Name.

```
PS> Get-Process -Name exp*,power*

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    540      15    35172      48148   141    88.44    408 explorer
    605       9    30668      29800   155     7.11   3052 powershell
```

Parametr ComputerName Get-Process můžete načíst procesy na vzdálených počítačích. Například následující příkaz získá postupy Powershellu v místním počítači (reprezentovaný identifikátorem "localhost") a na dvě vzdálené počítače.

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server02

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    258       8    29772      38636   130            3700 powershell
    398      24    75988      76800   572            5816 powershell
    605       9    30668      29800   155     7.11   3052 powershell
```

Názvy počítačů nejsou v tomto zobrazení zřejmé, ale jsou uložená ve vlastnosti MachineName procesu objektů, které vrátí Get-Process. Následující příkaz používá rutinu Format-Table k zobrazení ID procesu, ProcessName a MachineName (ComputerName) vlastnosti objektů process.

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server01 | Format-Table -Property ID, ProcessName, MachineName

  Id ProcessName MachineName
  -- ----------- -----------
3700 powershell  Server01
3052 powershell  Server02
5816 powershell  localhost
```

Složitější příkaz přidá vlastnost MachineName standardní zobrazení Get-Process.

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

## <a name="stopping-processes-stop-process"></a>Zastavuje se procesy (zastavit proces)

Prostředí Windows PowerShell poskytuje flexibilitu pro výpis procesů, ale co zastavení procesu?

**Stop-Process** rutina použije název nebo Id k určení procesu chcete zastavit. Možnost ukončit procesy závisí na vašich oprávněních. Nelze zastavit, některé procesy. Například pokud se pokusíte zastavte sledovací proces nečinné, dojde k chybě:

```
PS> Stop-Process -Name Idle
Stop-Process : Process 'Idle (0)' cannot be stopped due to the following error:
 Access is denied
At line:1 char:13
+ Stop-Process  <<<< -Name Idle
```

Můžete také vynutit dotazování se **potvrdit** parametru. Tento parametr je zvlášť užitečné, pokud používáte zástupný znak při zadávání názvu procesu, protože může nechtěně odpovídá některé procesy, které nechcete zastavit:

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

Pomocí některé z filtrování rutiny objektu je možné manipulaci s složitý proces. Protože objekt procesu má odpovídá vlastnost, která má hodnotu true, pokud již není aktivní, můžete zastavit všechny neodpovídající aplikace pomocí následujícího příkazu:

```powershell
Get-Process | Where-Object -FilterScript {$_.Responding -eq $false} | Stop-Process
```

Stejný přístup můžete použít v jiných situacích. Předpokládejme například, že aplikace sekundární oznamovací oblasti automaticky spustí, když uživatel spustí jinou aplikaci. Může se stát, že to nebude fungovat správně v relací Terminálové služby, ale chcete zachovat v relacích, které běží na konzole fyzického počítače. Relace připojení k desktopu fyzického počítače vždy mít ID relace 0, tak můžete zastavit všechny instance procesu, které jsou v jiných relacích pomocí **Where-Object** a procesu **SessionId** :

```powershell
Get-Process -Name BadApp | Where-Object -FilterScript {$_.SessionId -neq 0} | Stop-Process
```

Rutinu Stop-Process nemá parametr ComputerName. Proto se ke spuštění příkazu stop procesu ve vzdáleném počítači, budete muset použít rutiny Invoke-Command. Na vzdáleném počítači Server01 zastavte sledovací proces prostředí PowerShell, zadejte například:

```powershell
Invoke-Command -ComputerName Server01 {Stop-Process Powershell}
```

## <a name="stopping-all-other-windows-powershell-sessions"></a>Zastavuje se všechny ostatní relace Windows Powershellu

Čas od času může být užitečné umožnit zastavit všechny spuštěné relace Windows Powershellu než aktuální relaci. Pokud relace využívá příliš mnoho prostředků, nebo je nepřístupný (to však mohou používat vzdáleně, nebo v jiné relaci plochy), nebudete moci přímo zastavit. Při pokusu o zastavení všech spuštěných relací, ale aktuální relaci, mohou skončit.

Každé relaci prostředí Windows PowerShell obsahuje proměnné prostředí PID, který obsahuje Id procesu prostředí Windows PowerShell. Můžete zkontrolovat $PID pro Id každé relaci a ukončí pouze relace Windows Powershellu, které mají jiné Id. Pomocí následujícího příkazu kanál to dělá a vrátí seznam ukončení relace (protože se používá **PassThru** parametr):

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

## <a name="starting-debugging-and-waiting-for-processes"></a>Spuštění, ladění a čekání na procesy

Prostředí Windows PowerShell taky obsahuje rutiny start (nebo restartování), ladicí proces a počkejte na dokončení před spuštěním příkazu procesu. Informace o těchto rutinách najdete v tématu nápovědy rutiny pro každou rutinu.

## <a name="see-also"></a>Viz také

- [Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)
- [Stop-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)
- [Spustit proces](https://technet.microsoft.com/en-us/library/41a7e43c-9bb3-4dc2-8b0c-f6c32962e72c)
- [Wait – proces](https://technet.microsoft.com/en-us/library/9222af7a-789d-4a09-aa90-09d7c256c799)
- [Proces ladění](https://technet.microsoft.com/en-us/library/eea1dace-3913-4dbd-b659-5a94a610eee1)
- [Invoke-Command](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)
