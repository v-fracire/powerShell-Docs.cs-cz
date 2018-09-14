---
ms.date: 06/12/2017
keywords: jea, powershell, zabezpečení
title: Použití funkce JEA
ms.openlocfilehash: 539d280aff0b2656a5e9c710acfa468057753027
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522986"
---
# <a name="using-jea"></a>Použití funkce JEA

> Platí pro: Windows PowerShell 5.0

Toto téma popisuje různé způsoby se můžete připojit k a použití koncového bodu JEA.

## <a name="using-jea-interactively"></a>Použití interaktivní funkce JEA

Pokud testujete konfiguraci JEA nebo máte jednoduchých úloh pro uživatele k provedení, můžete použít JEA stejně jako byste to udělali regulární relaci vzdálené komunikace Powershellu.
Pro úlohy komplexní vzdálené komunikace se doporučuje používat [implicitní vzdálené komunikace](#using-jea-with-implicit-remoting) místo aby bylo snazší pro vaše uživatele tím, že uživatelé pracovat s data objekty místně.

Použití funkce JEA interaktivně, budete potřebovat:
- Název počítače, které se připojujete (může být místní počítač)
- Název koncového bodu JEA registrován na tomto počítači
- Přihlašovací údaje pro počítače, které mají přístup ke koncovému bodu JEA

Pomocí těchto informací v ručně, můžete začít používat relace JEA [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) nebo [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).

```powershell
$nonAdminCred = Get-Credential
Enter-PSSession -ComputerName localhost -ConfigurationName JEAMaintenance -Credential $nonAdminCred
```

Pokud účet, jste aktuálně přihlášeni jako má přístup ke koncovému bodu JEA, můžete vynechat `-Credential` parametru.

Pokud PowerShell vyzve změny `[localhost]: PS>` budete vědět, že je nyní interakci s JEA relace.
Můžete spustit `Get-Command` ke kontrole, které příkazy jsou k dispozici.
Musíte se obrátit se na správce a zjistěte, pokud existují nějaká omezení dostupné parametry nebo povolené parametr hodnoty.

Připomínáme JEA relace pracovat v NoLanguage režimu, takže některé ze způsobů, jak obvykle použijete PowerShell nemusí být k dispozici.
Například nemůžete použít proměnné k ukládání dat nebo kontrole vlastností objektů vrácených z rutin.
Následující příklad ukazuje příklad toho, jak využíváte prostředí PowerShell ještě dnes a dvou přístupů týkající se získání stejný příkaz funguje v režimu NoLanguage.

```powershell
# Using variables in NoLanguage mode is disallowed, so the following will not work
# $vm = Get-VM -Name 'SQL01'
# Start-VM -VM $vm

# You can use pipes to pass data through to commands that accept input from the pipeline
Get-VM -Name 'SQL01' | Start-VM

# You can also wrap subcommands in parentheses and enter them inline as arguments
Start-VM -VM (Get-VM -Name 'SQL01')

# Better yet, use parameter sets that don't require extra data to be passed in when possible
Start-VM -VMName 'SQL01'
```

Pro složitější vyvolání příkazu, kterým je tento přístup obtížné, zvažte použití [implicitní vzdálené komunikace](#using-jea-with-implicit-remoting) nebo [vytvoření vlastní funkce](role-capabilities.md#creating-custom-functions) zabalení, které vyžadujete funkce.

## <a name="using-jea-with-implicit-remoting"></a>Implicitní vzdálené komunikace pomocí funkce JEA

PowerShell podporuje model alternativní Vzdálená komunikace, ve kterém můžete importovat rutiny služby proxy ze vzdáleného počítače v místním počítači a s nimi pracovat, jako kdyby byly místní příkazy.
To se označuje implicitní vzdálené komunikace a je vysvětlené také v [to *Hey, Scripting Guy!* blogový příspěvek](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).
Implicitní vzdálené komunikace je užitečné při práci s JEA, protože umožňuje pracovat s rutinami JEA v režimu úplné jazyka.
To znamená, že používají dokončování pomocí tabulátoru, proměnné, manipulovat s objekty a dokonce i pomocí místní skripty snadněji automatizovat proti koncového bodu JEA.
Kdykoli můžete vyvolat příkaz proxy, data budou odeslány do koncového bodu JEA na vzdáleném počítači a spuštěny.

Implicitní vzdálené komunikace funguje tak, že rutiny Import z existující relace prostředí PowerShell.
Volitelně můžete jako předpona podstatná jména jednotlivých rutin proxy s řetězcem podle vašeho výběru k rozlišení, které příkazy jsou pro vzdálený systém.
Dočasný skript modulu, který obsahuje všechny příkazy proxy serveru se vytvoří a je možné po dobu trvání místní relaci Powershellu.

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Import the entire PSSession and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA'

# Invoke "Get-Command" on the remote JEA endpoint using the proxy cmdlet
Get-JEACommand
```

> [!IMPORTANT]
> Některé systémy nemusí být možné naimportovat celou relaci JEA z důvodu omezení v rutinách JEA výchozí.
> Chcete-li se tomuto problému vyhnout, importovat pouze příkazy potřebné z relace JEA explicitně zadáním jejich názvy k `-CommandName` parametru.
> Budoucí aktualizace se řešení potíží s importem celý JEA debaty ohrožených systémech.

Pokud nemůžete importovat JEA relace z důvodu omezení parametrů JEA výchozí, provedením následujících kroků, abyste odfiltrovat výchozí příkazy z importované sady.
Stále budete moci používat příkazů, jako jsou `Select-Object` – použijete jen místní verze nainstalovaná v počítači, ne vzdálené relace JEA.

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Get a list of all the commands on the JEA endpoint
$commands = Invoke-Command -Session $jeasession -ScriptBlock { Get-Command }

# Filter out the default cmdlets
$jeaDefaultCmdlets = 'Clear-Host', 'Exit-PSSession', 'Get-Command', 'Get-FormatData', 'Get-Help', 'Measure-Object', 'Out-Default', 'Select-Object'
$filteredCommands = $commands.Name | Where-Object { $jeaDefaultCmdlets -notcontains $_ }

# Import only commands explicitly added in role capabilities and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA' -CommandName $filteredCommands
```

Můžete také zachovat rutiny směrovány přes proxy server pomocí vzdálené komunikace implicitní [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).
Další informace o implicitní vzdálenou komunikaci, najdete v dokumentaci nápovědy [Import-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) a [Import-Module](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/import-module).

## <a name="using-jea-programatically"></a>Programově pomocí funkce JEA

JEA je také možné automatizace systémů a uživatelské aplikace, jako je například interní pracovník aplikací a webů.
Tento přístup je stejný jako, který k vytváření aplikací pro komunikaci s neomezeným koncových bodů prostředí PowerShell, s výstrahou, program měli vědět, že JEA je omezení příkazy, které lze spustit ve vzdálené relaci.

Pro jednoduché jednorázové úlohy, můžete použít [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command) ke spuštění sady příkazů pomocí JEA.

```powershell
Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Process; Get-Service }
```

Chcete-li zkontrolovat, které příkazy se dají používat, když se připojíte k relaci JEA, spusťte `Get-Command` a iterování přes výsledky ke kontrole povolených parametrů.

```powershell
$allowedCommands = Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Command }
$allowedCommands | Where-Object { $_.CommandType -in 'Function', 'Cmdlet' } | Format-Table Name, Parameters
```

Pokud vytváříte aplikaci C#, můžete vytvořit prostředí PowerShell prostředí runspace, který se připojuje k relaci JEA tak, že zadáte název konfigurace ve [WSManConnectionInfo](https://msdn.microsoft.com/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx) objektu.

```csharp

// using System.Management.Automation;
var computerName = "SERVER01";
var configName   = "JEAMaintenance";
var creds        = // create a PSCredential object here (https://msdn.microsoft.com/library/system.management.automation.pscredential(v=vs.85).aspx)

WSManConnectionInfo connectionInfo = new WSManConnectionInfo(
                    false,                 // Use SSL
                    computerName,          // Computer name
                    5985,                  // WSMan Port
                    "/wsman",              // WSMan Path
                    string.Format(CultureInfo.InvariantCulture, "http://schemas.microsoft.com/powershell/{0}", configName),  // Connection URI with config name
                    creds);                // Credentials
// Now, use the connection info to create a runspace where you can run the commands
using (Runspace runspace = RunspaceFactory.CreateRunspace(connectionInfo))
{
    // Open the runspace
    runspace.Open();

    using (PowerShell ps = PowerShell.Create())
    {
        // Set the PowerShell object to use the JEA runspace
        ps.Runspace = runspace;

        // Now you can add and invoke commands
        ps.AddCommand("Get-Command");
        foreach (var result in ps.Invoke())
        {
            Console.WriteLine(result);
        }
    }

    // Close the runspace
    runspace.Close();
}
```

## <a name="using-jea-with-powershell-direct"></a>Použití funkce JEA s přímou službu PowerShell

Technologie Hyper-V ve Windows 10 a Windows Server 2016 nabízí [přímou službu PowerShell](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/vmsession), funkci, která umožňuje správci technologie Hyper-V ke správě virtuálních počítačů pomocí Powershellu bez ohledu na konfiguraci sítě nebo vzdálené správy nastavení na virtuálním počítači.

Přímou službu PowerShell můžete použít s JEA poskytnout přístup omezený Správce technologie Hyper-V k vašemu virtuálnímu počítači, což může být užitečné, pokud ztratit připojení k síti k vašemu virtuálnímu počítači a správce datového centra potřebný k opravě nastavení sítě.

Žádná další konfigurace je potřeba použít JEA přes přímou službu PowerShell, ale operační systém spuštěný ve virtuálním počítači musí být Windows 10 nebo Windows Server 2016.
Správce technologie Hyper-V může připojit ke koncovému bodu JEA pomocí `-VMName` nebo `-VMId` parametrů v rutinách PSRemoting:

```powershell
# Entering a JEA session using PowerShell Direct when the VM name is unique
Enter-PSSession -VMName 'SQL01' -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'

# Entering a JEA session using PowerShell Direct using VM ids
$vm = Get-VM -VMName 'MyVM' | Select-Object -First 1
Enter-PSSession -VMId $vm.VMId -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'
```

Důrazně doporučujeme vytvořit jeden konkrétní uživatel místní s žádná jiná práva ke správě systému pro vaše Správce technologie Hyper-V použít.
Mějte na paměti, že jako Neprivilegovaný uživatel může stále přihlásit k počítači s Windows ve výchozím nastavení, včetně powershellu bez omezení.
Která umožní uživatelům procházet (některé z) v systému souborů a další informace o prostředí operačního systému.
Pro uzamčení správce technologie Hyper-V jenom přístup k virtuálnímu počítači pomocí funkce JEA přímou službu PowerShell, je potřeba zakázat místní přihlašovací práva pro účet JEA Správce technologie Hyper-V.