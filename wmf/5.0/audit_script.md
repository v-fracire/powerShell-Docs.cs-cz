---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: b8f175cee0a1de501b64890fdc2798f4f6421a14
ms.sourcegitcommit: 2ffb9fa92129c2001379ca2c17646466721f7165
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2018
ms.locfileid: "35251479"
---
# <a name="script-tracing-and-logging"></a><span data-ttu-id="814fb-102">Trasování a protokolování skriptu</span><span class="sxs-lookup"><span data-stu-id="814fb-102">Script Tracing and Logging</span></span>

<span data-ttu-id="814fb-103">Zatímco již obsahuje prostředí Windows PowerShell **LogPipelineExecutionDetails** zásad skupiny nastavení protokolu vyvolání rutiny, skriptovací jazyk pro PowerShell má hodně funkcí, které můžete chtít protokolování a auditování.</span><span class="sxs-lookup"><span data-stu-id="814fb-103">While Windows PowerShell already has the **LogPipelineExecutionDetails** Group Policy setting to log the invocation of cmdlets, PowerShell’s scripting language has plenty of features that you might want to log and/or audit.</span></span> <span data-ttu-id="814fb-104">Nové podrobné skriptu funkci pro trasování umožňuje povolit podrobné sledování a analýza skriptování použití prostředí Windows PowerShell v systému.</span><span class="sxs-lookup"><span data-stu-id="814fb-104">The new Detailed Script Tracing feature lets you enable detailed tracking and analysis of Windows PowerShell scripting use on a system.</span></span> <span data-ttu-id="814fb-105">Po povolení trasování podrobné skriptu prostředí Windows PowerShell zaznamená do protokolu událostí trasování událostí pro Windows, všechny bloky skriptu **Microsoft-Windows-PowerShell/Operational**.</span><span class="sxs-lookup"><span data-stu-id="814fb-105">After you enable detailed script tracing, Windows PowerShell logs all script blocks to the ETW event log, **Microsoft-Windows-PowerShell/Operational**.</span></span> <span data-ttu-id="814fb-106">Pokud blok skriptu vytvoří jiného bloku skriptu (například skript, který volá rutinu Invoke-Expression na řetězec), zaznamená se také že výsledné bloku skriptu.</span><span class="sxs-lookup"><span data-stu-id="814fb-106">If a script block creates another script block (for example, a script that calls the Invoke-Expression cmdlet on a string), that resulting script block is logged as well.</span></span>

<span data-ttu-id="814fb-107">Tyto události protokolování lze povolit prostřednictvím **zapnout protokolování bloku skriptu prostředí PowerShell** nastavení zásad skupiny (šablony pro správu -> součásti systému Windows -> prostředí Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="814fb-107">Logging of these events can be enabled through the **Turn on PowerShell Script Block Logging** Group Policy setting (in Administrative Templates -> Windows Components -> Windows PowerShell).</span></span>

<span data-ttu-id="814fb-108">Události jsou:</span><span class="sxs-lookup"><span data-stu-id="814fb-108">The events are:</span></span>

| <span data-ttu-id="814fb-109">Kanál</span><span class="sxs-lookup"><span data-stu-id="814fb-109">Channel</span></span> | <span data-ttu-id="814fb-110">Provozní</span><span class="sxs-lookup"><span data-stu-id="814fb-110">Operational</span></span>                                 |
|---------|---------------------------------------------|
| <span data-ttu-id="814fb-111">Úroveň</span><span class="sxs-lookup"><span data-stu-id="814fb-111">Level</span></span>   | <span data-ttu-id="814fb-112">Verbose</span><span class="sxs-lookup"><span data-stu-id="814fb-112">Verbose</span></span>                                     |
| <span data-ttu-id="814fb-113">Operační kód</span><span class="sxs-lookup"><span data-stu-id="814fb-113">Opcode</span></span>  | <span data-ttu-id="814fb-114">Create</span><span class="sxs-lookup"><span data-stu-id="814fb-114">Create</span></span>                                      |
| <span data-ttu-id="814fb-115">Úkol</span><span class="sxs-lookup"><span data-stu-id="814fb-115">Task</span></span>    | <span data-ttu-id="814fb-116">CommandStart</span><span class="sxs-lookup"><span data-stu-id="814fb-116">CommandStart</span></span>                                |
| <span data-ttu-id="814fb-117">– Klíčové slovo</span><span class="sxs-lookup"><span data-stu-id="814fb-117">Keyword</span></span> | <span data-ttu-id="814fb-118">Prostředí runspace</span><span class="sxs-lookup"><span data-stu-id="814fb-118">Runspace</span></span>                                    |
| <span data-ttu-id="814fb-119">ID události</span><span class="sxs-lookup"><span data-stu-id="814fb-119">EventId</span></span> | <span data-ttu-id="814fb-120">Engine_ScriptBlockCompiled (0x1008 = 4104)</span><span class="sxs-lookup"><span data-stu-id="814fb-120">Engine_ScriptBlockCompiled (0x1008 = 4104)</span></span>  |
| <span data-ttu-id="814fb-121">Zpráva</span><span class="sxs-lookup"><span data-stu-id="814fb-121">Message</span></span> | <span data-ttu-id="814fb-122">Vytváření textu Scriptblock (%1 typu %2):</span><span class="sxs-lookup"><span data-stu-id="814fb-122">Creating Scriptblock text (%1 of %2):</span></span> </br> <span data-ttu-id="814fb-123">%3</span><span class="sxs-lookup"><span data-stu-id="814fb-123">%3</span></span> </br> <span data-ttu-id="814fb-124">Blok skriptu ID: %4</span><span class="sxs-lookup"><span data-stu-id="814fb-124">ScriptBlock ID: %4</span></span> |


<span data-ttu-id="814fb-125">Rozsah bloku skriptu kompilovat, je text vložený do zprávy.</span><span class="sxs-lookup"><span data-stu-id="814fb-125">The text embedded in the message is the extent of the script block compiled.</span></span> <span data-ttu-id="814fb-126">ID je identifikátor GUID, který se uchovávají po dobu trvání blok skriptu.</span><span class="sxs-lookup"><span data-stu-id="814fb-126">The ID is a GUID that is retained for the life of the script block.</span></span>

<span data-ttu-id="814fb-127">Pokud povolíte podrobné protokolování, zápisů funkce začínat a končit značky:</span><span class="sxs-lookup"><span data-stu-id="814fb-127">When you enable verbose logging, the feature writes begin and end markers:</span></span>

| <span data-ttu-id="814fb-128">Kanál</span><span class="sxs-lookup"><span data-stu-id="814fb-128">Channel</span></span> | <span data-ttu-id="814fb-129">Provozní</span><span class="sxs-lookup"><span data-stu-id="814fb-129">Operational</span></span>                                            |
|---------|--------------------------------------------------------|
| <span data-ttu-id="814fb-130">Úroveň</span><span class="sxs-lookup"><span data-stu-id="814fb-130">Level</span></span>   | <span data-ttu-id="814fb-131">Verbose</span><span class="sxs-lookup"><span data-stu-id="814fb-131">Verbose</span></span>                                                |
| <span data-ttu-id="814fb-132">Operační kód</span><span class="sxs-lookup"><span data-stu-id="814fb-132">Opcode</span></span>  | <span data-ttu-id="814fb-133">Otevřete (/ zavřete)</span><span class="sxs-lookup"><span data-stu-id="814fb-133">Open (/ Close)</span></span>                                         |
| <span data-ttu-id="814fb-134">Úkol</span><span class="sxs-lookup"><span data-stu-id="814fb-134">Task</span></span>    | <span data-ttu-id="814fb-135">CommandStart (nebo CommandStop)</span><span class="sxs-lookup"><span data-stu-id="814fb-135">CommandStart (/ CommandStop)</span></span>                           |
| <span data-ttu-id="814fb-136">– Klíčové slovo</span><span class="sxs-lookup"><span data-stu-id="814fb-136">Keyword</span></span> | <span data-ttu-id="814fb-137">Prostředí runspace</span><span class="sxs-lookup"><span data-stu-id="814fb-137">Runspace</span></span>                                               |
| <span data-ttu-id="814fb-138">ID události</span><span class="sxs-lookup"><span data-stu-id="814fb-138">EventId</span></span> | <span data-ttu-id="814fb-139">Blok skriptu\_vyvolání\_spustit\_(0x1009 = 4105) podrobností /</span><span class="sxs-lookup"><span data-stu-id="814fb-139">ScriptBlock\_Invoke\_Start\_Detail (0x1009 = 4105) /</span></span> </br> <span data-ttu-id="814fb-140">Blok skriptu\_vyvolání\_dokončení\_(0x100A = 4106) podrobností</span><span class="sxs-lookup"><span data-stu-id="814fb-140">ScriptBlock\_Invoke\_Complete\_Detail (0x100A = 4106)</span></span> |
| <span data-ttu-id="814fb-141">Zpráva</span><span class="sxs-lookup"><span data-stu-id="814fb-141">Message</span></span> | <span data-ttu-id="814fb-142">Začínáme (/ dokončené) vyvolání ScriptBlock ID: %1</span><span class="sxs-lookup"><span data-stu-id="814fb-142">Started (/ Completed) invocation of ScriptBlock ID: %1</span></span> </br> <span data-ttu-id="814fb-143">Prostředí runspace ID: %2</span><span class="sxs-lookup"><span data-stu-id="814fb-143">Runspace ID: %2</span></span> |

<span data-ttu-id="814fb-144">ID je identifikátor GUID představující bloku skriptu (který může být korelační s ID události 0x1008) a prostředí Runspace ID představuje prostředí runspace, ve kterém byl spuštěn tento blok skriptu.</span><span class="sxs-lookup"><span data-stu-id="814fb-144">The ID is the GUID representing the script block (that can be correlated with event ID 0x1008), and the Runspace ID represents the runspace in which this script block was run.</span></span>

<span data-ttu-id="814fb-145">Znaky procenta ve zprávě volání představují strukturovaných vlastnosti trasování událostí pro Windows.</span><span class="sxs-lookup"><span data-stu-id="814fb-145">Percent signs in the invocation message represent structured ETW properties.</span></span> <span data-ttu-id="814fb-146">Když jsou nahrazeny skutečnými hodnotami v text zprávy, robustnější způsob, jak přistupovat k nim je načíst zprávu pomocí rutiny Get-WinEvent a potom pomocí **vlastnosti** pole zprávy.</span><span class="sxs-lookup"><span data-stu-id="814fb-146">While they are replaced with the actual values in the message text, a more robust way to access them is to retrieve the message with the Get-WinEvent cmdlet, and then use the **Properties** array of the message.</span></span>

<span data-ttu-id="814fb-147">Tady je příklad, jak můžete tuto funkci nápovědy k rozbalení škodlivý pokus o šifrování a obfuskováním skript:</span><span class="sxs-lookup"><span data-stu-id="814fb-147">Here's an example of how this functionality can help unwrap a malicious attempt to encrypt and obfuscate a script:</span></span>

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

<span data-ttu-id="814fb-148">Spuštění to generuje následující položky protokolu:</span><span class="sxs-lookup"><span data-stu-id="814fb-148">Running this generates the following log entries:</span></span>

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

Pokud délka bloku skriptu překročí, co je schopen uložení v jedné události trasování událostí pro Windows, prostředí Windows PowerShell skriptu dělí do několika částí. <span data-ttu-id="814fb-150">Tady je ukázkový kód pro změně kombinací skript z jeho zprávy protokolu:</span><span class="sxs-lookup"><span data-stu-id="814fb-150">Here is sample code to recombine a script from its log messages:</span></span>

```powershell
$created = Get-WinEvent -FilterHashtable @{ ProviderName="Microsoft-Windows-PowerShell"; Id = 4104 } | Where-Object { $_.<...> }
$sortedScripts = $created | sort { $_.Properties[0].Value }
$mergedScript = -join ($sortedScripts | % { $_.Properties[2].Value })
```

<span data-ttu-id="814fb-151">Stejně jako u všech systémů protokolování, které mají omezenou uchování vyrovnávací paměti (tj. protokoly trasování událostí pro Windows), jsou jeden útoky na tuto infrastrukturu k vyplnění protokolu s nesprávné události ke skrytí starší důkaz.</span><span class="sxs-lookup"><span data-stu-id="814fb-151">As with all logging systems that have a limited retention buffer (i.e. ETW logs), one attack against this infrastructure is to flood the log with spurious events to hide earlier evidence.</span></span> <span data-ttu-id="814fb-152">Ochranu před tento útok, ujistěte se, že máte určitou formu protokolu událostí kolekce nastavení pro zařízení (tj, předávání událostí systému Windows, [sledování nežádoucí osoba s monitorování protokolu událostí systému Windows](https://www.iad.gov/iad/library/reports/spotting-the-adversary-with-windows-event-log-monitoring.cfm)) přesunout protokoly událostí z počítače, jako v nejbližší době.</span><span class="sxs-lookup"><span data-stu-id="814fb-152">To protect yourself from this attack, ensure that you have some form of event log collection set up (i.e., Windows Event Forwarding, [Spotting the Adversary with Windows Event Log Monitoring](https://www.iad.gov/iad/library/reports/spotting-the-adversary-with-windows-event-log-monitoring.cfm)) to move event logs off of the computer as soon as possible.</span></span>
