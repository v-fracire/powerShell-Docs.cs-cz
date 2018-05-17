---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 2627b9d02788bd31a5384587406df533faf2cfaf
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="script-tracing-and-logging"></a>Trasování a protokolování skriptu

Zatímco již obsahuje prostředí Windows PowerShell **LogPipelineExecutionDetails** zásad skupiny nastavení protokolu vyvolání rutiny, skriptovací jazyk pro PowerShell má hodně funkcí, které můžete chtít protokolování a auditování. Nové podrobné skriptu funkci pro trasování umožňuje povolit podrobné sledování a analýza skriptování použití prostředí Windows PowerShell v systému. Po povolení trasování podrobné skriptu prostředí Windows PowerShell zaznamená do protokolu událostí trasování událostí pro Windows, všechny bloky skriptu **Microsoft-Windows-PowerShell/Operational**. Pokud blok skriptu vytvoří jiného bloku skriptu (například skript, který volá rutinu Invoke-Expression na řetězec), zaznamená se také že výsledné bloku skriptu.

Tyto události protokolování lze povolit prostřednictvím **zapnout protokolování bloku skriptu prostředí PowerShell** nastavení zásad skupiny (šablony pro správu -> součásti systému Windows -> prostředí Windows PowerShell).

Události jsou:

| Kanál | Provozní                                 |
|---------|---------------------------------------------|
| Úroveň   | Verbose                                     |
| Operační kód  | Create                                      |
| Úkol    | CommandStart                                |
| – Klíčové slovo | Prostředí runspace                                    |
| ID události | Engine_ScriptBlockCompiled (0x1008 = 4104)  |
| Zpráva | Vytváření textu Scriptblock (%1 typu %2): </br> %3 </br> Blok skriptu ID: %4 |


Rozsah bloku skriptu kompilovat, je text vložený do zprávy. ID je identifikátor GUID, který se uchovávají po dobu trvání blok skriptu.

Pokud povolíte podrobné protokolování, zápisů funkce začínat a končit značky:

| Kanál | Provozní                                            |
|---------|--------------------------------------------------------|
| Úroveň   | Verbose                                                |
| Operační kód  | Otevřete (/ zavřete)                                         |
| Úkol    | CommandStart (nebo CommandStop)                           |
| – Klíčové slovo | Prostředí runspace                                               |
| ID události | Blok skriptu\_vyvolání\_spustit\_(0x1009 = 4105) podrobností / </br> Blok skriptu\_vyvolání\_dokončení\_(0x100A = 4106) podrobností |
| Zpráva | Začínáme (/ dokončené) vyvolání ScriptBlock ID: %1 </br> Prostředí runspace ID: %2 |

ID je identifikátor GUID představující bloku skriptu (který může být korelační s ID události 0x1008) a prostředí Runspace ID představuje prostředí runspace, ve kterém byl spuštěn tento blok skriptu.

Znaky procenta ve zprávě volání představují strukturovaných vlastnosti trasování událostí pro Windows. Když jsou nahrazeny skutečnými hodnotami v text zprávy, robustnější způsob, jak přistupovat k nim je načíst zprávu pomocí rutiny Get-WinEvent a potom pomocí **vlastnosti** pole zprávy.

Tady je příklad, jak můžete tuto funkci nápovědy k rozbalení škodlivý pokus o šifrování a obfuskováním skript:

```powershell
## Malware
function SuperDecrypt
{
    param($script)
    $bytes = [Convert]::FromBase64String($script)

    ## XOR “encryption”
    $xorKey = 0x42
    for($counter = 0; $counter -lt $bytes.Length; $counter++)
    {
        $bytes[$counter] = $bytes[$counter] -bxor $xorKey
    }
    [System.Text.Encoding]::Unicode.GetString($bytes)
}

$decrypted = SuperDecrypt "FUIwQitCNkInQm9CCkItQjFCNkJiQmVCEkI1QixCJkJlQg=="
Invoke-Expression $decrypted
```

Spuštění to generuje následující položky protokolu:

```
Compiling Scriptblock text (1 of 1):
function SuperDecrypt
{
    param($script)
    $bytes = [Convert]::FromBase64String($script)
    ## XOR "encryption"
    $xorKey = 0x42
    for($counter = 0; $counter -lt $bytes.Length; $counter++)
    {
        $bytes[$counter] = $bytes[$counter] -bxor $xorKey
    }
    [System.Text.Encoding]::Unicode.GetString($bytes)

}
ScriptBlock ID: ad8ae740-1f33-42aa-8dfc-1314411877e3

Compiling Scriptblock text (1 of 1):
$decrypted = SuperDecrypt "FUIwQitCNkInQm9CCkItQjFCNkJiQmVCEkI1QixCJkJlQg=="
ScriptBlock ID: ba11c155-d34c-4004-88e3-6502ecb50f52

Compiling Scriptblock text (1 of 1):
Invoke-Expression $decrypted
ScriptBlock ID: 856c01ca-85d7-4989-b47f-e6a09ee4eeb3

Compiling Scriptblock text (1 of 1):
Write-Host 'Pwnd'
ScriptBlock ID: 5e618414-4e77-48e3-8f65-9a863f54b4c8
```

Pokud délka bloku skriptu překročí, co je schopen uložení v jedné události trasování událostí pro Windows, prostředí Windows PowerShell skriptu dělí do několika částí. Tady je ukázkový kód pro změně kombinací skript z jeho zprávy protokolu:

```powershell
$created = Get-WinEvent -FilterHashtable @{ ProviderName="Microsoft-Windows-PowerShell"; Id = 4104 } | Where-Object { $_.<...> }
$sortedScripts = $created | sort { $_.Properties[0].Value }
$mergedScript = -join ($sortedScripts | % { $_.Properties[2].Value })
```

Stejně jako u všech systémů protokolování, které mají omezenou uchování vyrovnávací paměti (tj. protokoly trasování událostí pro Windows), jsou jeden útoky na tuto infrastrukturu k vyplnění protokolu s nesprávné události ke skrytí starší důkaz. Ochranu před tento útok, ujistěte se, že máte určitou formu protokolu událostí kolekce nastavení pro zařízení (tj, předávání událostí systému Windows, [sledování nežádoucí osoba s monitorování protokolu událostí systému Windows](http://www.nsa.gov/ia/_files/app/Spotting_the_Adversary_with_Windows_Event_Log_Monitoring.pdf)) přesunout protokoly událostí z počítače, jako v nejbližší době.
