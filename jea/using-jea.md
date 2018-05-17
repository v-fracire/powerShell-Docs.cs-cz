---
ms.date: 06/12/2017
keywords: jea, prostředí powershell, zabezpečení
title: Použití funkce JEA
ms.openlocfilehash: 891e4be4c3fadceeff5ede7ac5cab04a5f80e5c1
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="using-jea"></a>Použití funkce JEA

> Platí pro: prostředí Windows PowerShell 5.0

Toto téma popisuje různé způsoby, kterými můžete připojit k a používání JEA koncového bodu.

## <a name="using-jea-interactively"></a>Pomocí JEA interaktivně

Pokud testujete konfiguraci JEA nebo mají jednoduché úlohy pro uživatele k provedení, můžete použít JEA stejným způsobem, jako by relaci regulární vzdálenou komunikaci prostředí PowerShell.
Pro úlohy, komplexní vzdálenou komunikaci, doporučuje se použít [implicitní vzdálenou komunikaci](#using-jea-with-implicit-remoting) místo aby bylo snazší pro vaše uživatele tím, že se uživatelům pracovat s data objekty místně.

Pokud chcete používat JEA interaktivně, budete potřebovat:
- Název počítače, kam se připojujete (může být místní počítač)
- Název koncového bodu JEA registrovány na tomto počítači
- Pověření pro tento počítač, které mají přístup ke koncovému bodu JEA

Tyto informace v dolním můžete spouštět pomocí relace JEA [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) nebo [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).

```powershell
$nonAdminCred = Get-Credential
Enter-PSSession -ComputerName localhost -ConfigurationName JEAMaintenance -Credential $nonAdminCred
```

Pokud jste aktuálně přihlášeni jako má přístup ke koncovému bodu JEA účet, můžete vynechat `-Credential` parametr.

Pokud PowerShell vyzve změny `[localhost]: PS>` budete vědět, že je nyní interakci s JEA relace.
Můžete spustit `Get-Command` ke kontrole, které příkazy, které jsou k dispozici.
Musíte se obrátit se na správce a zjistěte, pokud existují nějaká omezení na dostupné parametry nebo hodnoty parametru povolená.

Připomínáme JEA relací fungovat v režimu NoLanguage, proto některé způsoby, obvykle pomocí prostředí PowerShell pravděpodobně není k dispozici.
Proměnné pro instanci nelze použít k ukládání dat nebo zkontrolujte vlastností u objektů vrácených z rutiny.
Následující příklad znázorňuje příklad toho, jak vám může být pomocí prostředí PowerShell ještě dnes, a dva přístupy k získání stejný příkaz práce v režimu NoLanguage.

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

Pro složitější příkaz volání, které tento přístup velmi obtížné, zvažte použití [implicitní vzdálenou komunikaci](#using-jea-with-implicit-remoting) nebo [vytvoření vlastní funkce](role-capabilities.md#creating-custom-functions) , zabalení funkci požadavky.

## <a name="using-jea-with-implicit-remoting"></a>JEA pomocí implicitní vzdálené komunikace

Prostředí PowerShell podporuje model alternativní vzdálenou komunikaci, kde můžete importovat rutiny služby proxy ze vzdáleného počítače v místním počítači a s nimi pracovat, jako kdyby byly místní příkazy.
To se označuje jako implicitní vzdálenou komunikaci a je vysvětleno v dobře [to *blogu Hey, Scripting Guy!* příspěvku na blogu](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).
Implicitní vzdálené komunikace je zvláště užitečná při práci s JEA, protože umožňuje pracovat s rutinami JEA v režimu úplné jazyk.
To znamená, že můžete využít dokončování pomocí tabulátorů, proměnné, pracovat s objekty a i pomocí místní skripty pro automatizaci snadněji koncový bod JEA.
Kdykoliv vyvolání příkazu proxy, data budou odeslány do koncového bodu JEA ve vzdáleném počítači a provést existuje.

Implicitní vzdálenou komunikaci funguje tak, že import rutiny z existující relace prostředí PowerShell.
Volitelně můžete předpony podstatná jména každou rutinu proxy řetězcem dle vlastního výběru k rozlišení, které příkazy jsou pro vzdálený systém.
Modul dočasný skript obsahující všechny příkazy proxy serveru se vytvoří a lze použít pro dobu trvání místní relace prostředí PowerShell.

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Import the entire PSSession and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA'

# Invoke "Get-Command" on the remote JEA endpoint using the proxy cmdlet
Get-JEACommand
```

> [!IMPORTANT]
> Některé systémy nemusí být možné importovat celé relace JEA z důvodu omezení v rutinách JEA výchozí.
> Chcete-li se tomuto problému vyhnout, importovat pouze příkazy, je nutné z relace JEA explicitně zadáním jejich názvy na `-CommandName` parametr.
> Budoucí aktualizace se vyřešit problém s importem celý JEA relací v ovlivněných systémech.

Pokud nebylo možné importovat relaci JEA z důvodu omezení na výchozí JEA parametry, můžete postupujte podle následujících kroků a odfiltrovat výchozí příkazy v importované sadě.
Stále nebudete moci používat příkazy, jako je `Select-Object` – stačí použijete místní verze nainstalovaná v počítači místo vzdálené jeden v relaci JEA.

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

Můžete také zachovat rutiny směrovány přes proxy server pomocí implicitní vzdálenou komunikaci [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).
Další informace o implicitní vzdálenou komunikaci, najdete v dokumentaci nápovědy [Import-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) a [Import-Module](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/import-module).

## <a name="using-jea-programatically"></a>Programově pomocí JEA

JEA mohou sloužit také v systémech automation a v uživatelské aplikace, jako třeba interní pracovník aplikace a webové servery.
Přístup je stejný, jako který pro vytváření aplikací, které komunikují s neomezeným koncových bodů prostředí PowerShell, přímý přístup do paměti, že program měli vědět, že JEA je omezení příkazy, které se může spouštět ve vzdálené relaci.

Pro jednoduché, jednorázové úlohy, můžete použít [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command) ke spuštění sady příkazů pomocí JEA.

```powershell
Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Process; Get-Service }
```

Chcete-li zkontrolovat, které příkazy jsou k dispozici pro použití při připojování k relaci JEA, spusťte `Get-Command` a iterovat výsledky zkontrolujte povolené parametry.

```powershell
$allowedCommands = Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Command }
$allowedCommands | Where-Object { $_.CommandType -in 'Function', 'Cmdlet' } | Format-Table Name, Parameters
```

Pokud vytváříte aplikace C#, můžete vytvořit prostředí runspace prostředí PowerShell, která se připojuje k relaci JEA tak, že zadáte název konfigurace ve [WSManConnectionInfo](https://msdn.microsoft.com/en-us/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx) objektu.

```csharp

// using System.Management.Automation;
var computerName = "SERVER01";
var configName   = "JEAMaintenance";
var creds        = // create a PSCredential object here (https://msdn.microsoft.com/en-us/library/system.management.automation.pscredential(v=vs.85).aspx)

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

## <a name="using-jea-with-powershell-direct"></a>Pomocí prostředí PowerShell přímo JEA

Nabízí technologie Hyper-V v systému Windows 10 a Windows Server 2016 [prostředí PowerShell přímo](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/user_guide/vmsession), funkci, která umožňuje správci Hyper-V ke správě virtuálních počítačů bez ohledu na konfiguraci sítě nebo vzdálené správy pomocí prostředí PowerShell nastavení na virtuálním počítači.

Prostředí PowerShell přímo s JEA vám pomůže poskytnout přístup omezený Správce technologie Hyper-V k virtuálnímu počítači, což může být užitečné, pokud ztratit připojení k síti pro virtuální počítač a musí správce datového centra opravte nastavení sítě.

Žádná další konfigurace se vyžaduje použití JEA přes PowerShell přímo, ale operační systém spuštěný ve virtuálním počítači musí být Windows 10 nebo Windows Server 2016.
Správce technologie Hyper-V můžete připojit ke koncovému bodu JEA pomocí `-VMName` nebo `-VMId` parametry rutiny PSRemoting:

```powershell
# Entering a JEA session using PowerShell Direct when the VM name is unique
Enter-PSSession -VMName 'SQL01' -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'

# Entering a JEA session using PowerShell Direct using VM ids
$vm = Get-VM -VMName 'MyVM' | Select-Object -First 1
Enter-PSSession -VMId $vm.VMId -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'
```

Důrazně doporučujeme vytvořit vyhrazený místního uživatele s žádná práva ke správě systému pro správce technologie Hyper-V použít.
Mějte na paměti, že i Neprivilegovaný uživatel může stále přihlásit do počítače s Windows ve výchozím nastavení, včetně použití neomezeným prostředí PowerShell.
Které umožní uživatelům procházet (část) systému souborů a další informace o prostředí operačního systému.
Zamknout Správce technologie Hyper-V jenom přístup k virtuálnímu počítači pomocí prostředí PowerShell přímo JEA, musíte se tak, aby odepřel práva místního přihlášení k účtu JEA Správce technologie Hyper-V.