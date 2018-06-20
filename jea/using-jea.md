---
ms.date: 06/12/2017
keywords: jea, prostředí powershell, zabezpečení
title: Použití funkce JEA
ms.openlocfilehash: 891e4be4c3fadceeff5ede7ac5cab04a5f80e5c1
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34190073"
---
# <a name="using-jea"></a><span data-ttu-id="27ab5-103">Použití funkce JEA</span><span class="sxs-lookup"><span data-stu-id="27ab5-103">Using JEA</span></span>

> <span data-ttu-id="27ab5-104">Platí pro: prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="27ab5-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="27ab5-105">Toto téma popisuje různé způsoby, kterými můžete připojit k a používání JEA koncového bodu.</span><span class="sxs-lookup"><span data-stu-id="27ab5-105">This topic describes the various ways you can connect to and use a JEA endpoint.</span></span>

## <a name="using-jea-interactively"></a><span data-ttu-id="27ab5-106">Pomocí JEA interaktivně</span><span class="sxs-lookup"><span data-stu-id="27ab5-106">Using JEA interactively</span></span>

<span data-ttu-id="27ab5-107">Pokud testujete konfiguraci JEA nebo mají jednoduché úlohy pro uživatele k provedení, můžete použít JEA stejným způsobem, jako by relaci regulární vzdálenou komunikaci prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27ab5-107">If you are testing your JEA configuration or have simple tasks for users to perform, you can use JEA the same way you would a regular PowerShell remoting session.</span></span>
<span data-ttu-id="27ab5-108">Pro úlohy, komplexní vzdálenou komunikaci, doporučuje se použít [implicitní vzdálenou komunikaci](#using-jea-with-implicit-remoting) místo aby bylo snazší pro vaše uživatele tím, že se uživatelům pracovat s data objekty místně.</span><span class="sxs-lookup"><span data-stu-id="27ab5-108">For complex remoting tasks, it is recommended to use [implicit remoting](#using-jea-with-implicit-remoting) instead to make it easier for your users by allowing users to operate with the data objects locally.</span></span>

<span data-ttu-id="27ab5-109">Pokud chcete používat JEA interaktivně, budete potřebovat:</span><span class="sxs-lookup"><span data-stu-id="27ab5-109">To use JEA interactively, you will need:</span></span>
- <span data-ttu-id="27ab5-110">Název počítače, kam se připojujete (může být místní počítač)</span><span class="sxs-lookup"><span data-stu-id="27ab5-110">The name of the computer you are connecting to (can be the local machine)</span></span>
- <span data-ttu-id="27ab5-111">Název koncového bodu JEA registrovány na tomto počítači</span><span class="sxs-lookup"><span data-stu-id="27ab5-111">The name of the JEA endpoint registered on that computer</span></span>
- <span data-ttu-id="27ab5-112">Pověření pro tento počítač, které mají přístup ke koncovému bodu JEA</span><span class="sxs-lookup"><span data-stu-id="27ab5-112">Credentials for the computer that have access to the JEA endpoint</span></span>

<span data-ttu-id="27ab5-113">Tyto informace v dolním můžete spouštět pomocí relace JEA [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) nebo [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).</span><span class="sxs-lookup"><span data-stu-id="27ab5-113">With that information in hand, you can start a JEA session using [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) or [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).</span></span>

```powershell
$nonAdminCred = Get-Credential
Enter-PSSession -ComputerName localhost -ConfigurationName JEAMaintenance -Credential $nonAdminCred
```

<span data-ttu-id="27ab5-114">Pokud jste aktuálně přihlášeni jako má přístup ke koncovému bodu JEA účet, můžete vynechat `-Credential` parametr.</span><span class="sxs-lookup"><span data-stu-id="27ab5-114">If the account you're currently logged in as has access to the JEA endpoint, you can omit the `-Credential` parameter.</span></span>

<span data-ttu-id="27ab5-115">Pokud PowerShell vyzve změny `[localhost]: PS>` budete vědět, že je nyní interakci s JEA relace.</span><span class="sxs-lookup"><span data-stu-id="27ab5-115">When the PowerShell prompt changes to `[localhost]: PS>` you will know that you are now interacting with the remote JEA session.</span></span>
<span data-ttu-id="27ab5-116">Můžete spustit `Get-Command` ke kontrole, které příkazy, které jsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="27ab5-116">You can run `Get-Command` to check which commands are available.</span></span>
<span data-ttu-id="27ab5-117">Musíte se obrátit se na správce a zjistěte, pokud existují nějaká omezení na dostupné parametry nebo hodnoty parametru povolená.</span><span class="sxs-lookup"><span data-stu-id="27ab5-117">You will need to consult with your administrator to learn if there are any restrictions on the available parameters or allowable parameter values.</span></span>

<span data-ttu-id="27ab5-118">Připomínáme JEA relací fungovat v režimu NoLanguage, proto některé způsoby, obvykle pomocí prostředí PowerShell pravděpodobně není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="27ab5-118">As a reminder, JEA sessions operate in NoLanguage mode, so some of the ways you typically use PowerShell may not be available.</span></span>
<span data-ttu-id="27ab5-119">Proměnné pro instanci nelze použít k ukládání dat nebo zkontrolujte vlastností u objektů vrácených z rutiny.</span><span class="sxs-lookup"><span data-stu-id="27ab5-119">For instance, you cannot use variables to store data or inspect the properties on objects returned from cmdlets.</span></span>
<span data-ttu-id="27ab5-120">Následující příklad znázorňuje příklad toho, jak vám může být pomocí prostředí PowerShell ještě dnes, a dva přístupy k získání stejný příkaz práce v režimu NoLanguage.</span><span class="sxs-lookup"><span data-stu-id="27ab5-120">The below example shows an example of how you may be using PowerShell today, and two approaches to get the same command working in NoLanguage mode.</span></span>

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

<span data-ttu-id="27ab5-121">Pro složitější příkaz volání, které tento přístup velmi obtížné, zvažte použití [implicitní vzdálenou komunikaci](#using-jea-with-implicit-remoting) nebo [vytvoření vlastní funkce](role-capabilities.md#creating-custom-functions) , zabalení funkci požadavky.</span><span class="sxs-lookup"><span data-stu-id="27ab5-121">For more complex command invocations that make this approach difficult, consider using [implicit remoting](#using-jea-with-implicit-remoting) or [creating custom functions](role-capabilities.md#creating-custom-functions) that wrap the functionality you desire.</span></span>

## <a name="using-jea-with-implicit-remoting"></a><span data-ttu-id="27ab5-122">JEA pomocí implicitní vzdálené komunikace</span><span class="sxs-lookup"><span data-stu-id="27ab5-122">Using JEA with implicit remoting</span></span>

<span data-ttu-id="27ab5-123">Prostředí PowerShell podporuje model alternativní vzdálenou komunikaci, kde můžete importovat rutiny služby proxy ze vzdáleného počítače v místním počítači a s nimi pracovat, jako kdyby byly místní příkazy.</span><span class="sxs-lookup"><span data-stu-id="27ab5-123">PowerShell supports an alternative remoting model where you can import proxy cmdlets from a remote machine on your local computer and interact with them as if they were local commands.</span></span>
<span data-ttu-id="27ab5-124">To se označuje jako implicitní vzdálenou komunikaci a je vysvětleno v dobře [to *blogu Hey, Scripting Guy!* příspěvku na blogu](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).</span><span class="sxs-lookup"><span data-stu-id="27ab5-124">This is called implicit remoting, and is explained well in [this *Hey, Scripting Guy!* blog post](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).</span></span>
<span data-ttu-id="27ab5-125">Implicitní vzdálené komunikace je zvláště užitečná při práci s JEA, protože umožňuje pracovat s rutinami JEA v režimu úplné jazyk.</span><span class="sxs-lookup"><span data-stu-id="27ab5-125">Implicit remoting is particularly useful when working with JEA because it allows you to work with JEA cmdlets in a full language mode.</span></span>
<span data-ttu-id="27ab5-126">To znamená, že můžete využít dokončování pomocí tabulátorů, proměnné, pracovat s objekty a i pomocí místní skripty pro automatizaci snadněji koncový bod JEA.</span><span class="sxs-lookup"><span data-stu-id="27ab5-126">This means you can use tab completion, variables, manipulate objects, and even use local scripts to more easily automate against a JEA endpoint.</span></span>
<span data-ttu-id="27ab5-127">Kdykoliv vyvolání příkazu proxy, data budou odeslány do koncového bodu JEA ve vzdáleném počítači a provést existuje.</span><span class="sxs-lookup"><span data-stu-id="27ab5-127">Anytime you invoke a proxy command, the data will be sent to the JEA endpoint on the remote machine and executed there.</span></span>

<span data-ttu-id="27ab5-128">Implicitní vzdálenou komunikaci funguje tak, že import rutiny z existující relace prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27ab5-128">Implicit remoting works by importing cmdlets from an existing PowerShell session.</span></span>
<span data-ttu-id="27ab5-129">Volitelně můžete předpony podstatná jména každou rutinu proxy řetězcem dle vlastního výběru k rozlišení, které příkazy jsou pro vzdálený systém.</span><span class="sxs-lookup"><span data-stu-id="27ab5-129">You can optionally choose to prefix the nouns of each proxy cmdlet with a string of your choosing to distinguish which commands are for the remote system.</span></span>
<span data-ttu-id="27ab5-130">Modul dočasný skript obsahující všechny příkazy proxy serveru se vytvoří a lze použít pro dobu trvání místní relace prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27ab5-130">A temporary script module containing all of the proxy commands will be created and can be used for the duration of your local PowerShell session.</span></span>

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Import the entire PSSession and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA'

# Invoke "Get-Command" on the remote JEA endpoint using the proxy cmdlet
Get-JEACommand
```

> [!IMPORTANT]
> <span data-ttu-id="27ab5-131">Některé systémy nemusí být možné importovat celé relace JEA z důvodu omezení v rutinách JEA výchozí.</span><span class="sxs-lookup"><span data-stu-id="27ab5-131">Some systems may not be able to import an entire JEA session due to constraints in the default JEA cmdlets.</span></span>
> <span data-ttu-id="27ab5-132">Chcete-li se tomuto problému vyhnout, importovat pouze příkazy, je nutné z relace JEA explicitně zadáním jejich názvy na `-CommandName` parametr.</span><span class="sxs-lookup"><span data-stu-id="27ab5-132">To get around this, only import the commands you need from the JEA session by explicitly providing their names to the `-CommandName` parameter.</span></span>
> <span data-ttu-id="27ab5-133">Budoucí aktualizace se vyřešit problém s importem celý JEA relací v ovlivněných systémech.</span><span class="sxs-lookup"><span data-stu-id="27ab5-133">A future update will address the issue with importing entire JEA sessions on affected systems.</span></span>

<span data-ttu-id="27ab5-134">Pokud nebylo možné importovat relaci JEA z důvodu omezení na výchozí JEA parametry, můžete postupujte podle následujících kroků a odfiltrovat výchozí příkazy v importované sadě.</span><span class="sxs-lookup"><span data-stu-id="27ab5-134">If you are unable to import a JEA session due to constraints on the default JEA parameters, you can follow the steps below to filter out the default commands from the imported set.</span></span>
<span data-ttu-id="27ab5-135">Stále nebudete moci používat příkazy, jako je `Select-Object` – stačí použijete místní verze nainstalovaná v počítači místo vzdálené jeden v relaci JEA.</span><span class="sxs-lookup"><span data-stu-id="27ab5-135">You will still be able to use commands like `Select-Object` -- you'll just use the local version installed on your computer instead of the remote one in the JEA session.</span></span>

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

<span data-ttu-id="27ab5-136">Můžete také zachovat rutiny směrovány přes proxy server pomocí implicitní vzdálenou komunikaci [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).</span><span class="sxs-lookup"><span data-stu-id="27ab5-136">You can also persist the proxied cmdlets from implicit remoting using [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).</span></span>
<span data-ttu-id="27ab5-137">Další informace o implicitní vzdálenou komunikaci, najdete v dokumentaci nápovědy [Import-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) a [Import-Module](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/import-module).</span><span class="sxs-lookup"><span data-stu-id="27ab5-137">For more information about implicit remoting, check out the help documentation for [Import-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) and [Import-Module](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/import-module).</span></span>

## <a name="using-jea-programatically"></a><span data-ttu-id="27ab5-138">Programově pomocí JEA</span><span class="sxs-lookup"><span data-stu-id="27ab5-138">Using JEA programatically</span></span>

<span data-ttu-id="27ab5-139">JEA mohou sloužit také v systémech automation a v uživatelské aplikace, jako třeba interní pracovník aplikace a webové servery.</span><span class="sxs-lookup"><span data-stu-id="27ab5-139">JEA can also be used in automation systems and in user applications, such as in-house helpdesk apps and web sites.</span></span>
<span data-ttu-id="27ab5-140">Přístup je stejný, jako který pro vytváření aplikací, které komunikují s neomezeným koncových bodů prostředí PowerShell, přímý přístup do paměti, že program měli vědět, že JEA je omezení příkazy, které se může spouštět ve vzdálené relaci.</span><span class="sxs-lookup"><span data-stu-id="27ab5-140">The approach is the same as that for building apps that talk to unconstrained PowerShell endpoints, with the caveat that the program should be aware that JEA is limiting the commands that can be run in the remote session.</span></span>

<span data-ttu-id="27ab5-141">Pro jednoduché, jednorázové úlohy, můžete použít [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command) ke spuštění sady příkazů pomocí JEA.</span><span class="sxs-lookup"><span data-stu-id="27ab5-141">For simple, one-off tasks, you can use [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command) to run a set of commands using JEA.</span></span>

```powershell
Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Process; Get-Service }
```

<span data-ttu-id="27ab5-142">Chcete-li zkontrolovat, které příkazy jsou k dispozici pro použití při připojování k relaci JEA, spusťte `Get-Command` a iterovat výsledky zkontrolujte povolené parametry.</span><span class="sxs-lookup"><span data-stu-id="27ab5-142">To check which commands are available for use when you connect to a JEA session, run `Get-Command` and iterate through the results to check for the allowed parameters.</span></span>

```powershell
$allowedCommands = Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Command }
$allowedCommands | Where-Object { $_.CommandType -in 'Function', 'Cmdlet' } | Format-Table Name, Parameters
```

<span data-ttu-id="27ab5-143">Pokud vytváříte aplikace C#, můžete vytvořit prostředí runspace prostředí PowerShell, která se připojuje k relaci JEA tak, že zadáte název konfigurace ve [WSManConnectionInfo](https://msdn.microsoft.com/en-us/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx) objektu.</span><span class="sxs-lookup"><span data-stu-id="27ab5-143">If you are building a C# app, you can create a PowerShell runspace that connects to a JEA session by specifying the configuration name in a [WSManConnectionInfo](https://msdn.microsoft.com/en-us/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx) object.</span></span>

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

## <a name="using-jea-with-powershell-direct"></a><span data-ttu-id="27ab5-144">Pomocí prostředí PowerShell přímo JEA</span><span class="sxs-lookup"><span data-stu-id="27ab5-144">Using JEA with PowerShell Direct</span></span>

<span data-ttu-id="27ab5-145">Nabízí technologie Hyper-V v systému Windows 10 a Windows Server 2016 [prostředí PowerShell přímo](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/user_guide/vmsession), funkci, která umožňuje správci Hyper-V ke správě virtuálních počítačů bez ohledu na konfiguraci sítě nebo vzdálené správy pomocí prostředí PowerShell nastavení na virtuálním počítači.</span><span class="sxs-lookup"><span data-stu-id="27ab5-145">Hyper-V in Windows 10 and Windows Server 2016 offers [PowerShell Direct](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/user_guide/vmsession), a feature which allows Hyper-V administrators to manage virtual machines with PowerShell regardless of the network configuration or remote management settings on the virtual machine.</span></span>

<span data-ttu-id="27ab5-146">Prostředí PowerShell přímo s JEA vám pomůže poskytnout přístup omezený Správce technologie Hyper-V k virtuálnímu počítači, což může být užitečné, pokud ztratit připojení k síti pro virtuální počítač a musí správce datového centra opravte nastavení sítě.</span><span class="sxs-lookup"><span data-stu-id="27ab5-146">You can use PowerShell Direct with JEA to give a Hyper-V administrator limited access to your VM, which can be useful if you lose network connectivity to your VM and need a datacenter admin to fix the network settings.</span></span>

<span data-ttu-id="27ab5-147">Žádná další konfigurace se vyžaduje použití JEA přes PowerShell přímo, ale operační systém spuštěný ve virtuálním počítači musí být Windows 10 nebo Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="27ab5-147">No additional configuration is required to use JEA over PowerShell Direct, however the operating system running inside the virtual machine must be Windows 10 or Windows Server 2016.</span></span>
<span data-ttu-id="27ab5-148">Správce technologie Hyper-V můžete připojit ke koncovému bodu JEA pomocí `-VMName` nebo `-VMId` parametry rutiny PSRemoting:</span><span class="sxs-lookup"><span data-stu-id="27ab5-148">The Hyper-V admin can connect to the JEA endpoint by using the `-VMName` or `-VMId` parameters on PSRemoting cmdlets:</span></span>

```powershell
# Entering a JEA session using PowerShell Direct when the VM name is unique
Enter-PSSession -VMName 'SQL01' -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'

# Entering a JEA session using PowerShell Direct using VM ids
$vm = Get-VM -VMName 'MyVM' | Select-Object -First 1
Enter-PSSession -VMId $vm.VMId -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'
```

<span data-ttu-id="27ab5-149">Důrazně doporučujeme vytvořit vyhrazený místního uživatele s žádná práva ke správě systému pro správce technologie Hyper-V použít.</span><span class="sxs-lookup"><span data-stu-id="27ab5-149">It is strongly recommended that you create a dedicated local user with no other rights to manage the system for your Hyper-V administrators to use.</span></span>
<span data-ttu-id="27ab5-150">Mějte na paměti, že i Neprivilegovaný uživatel může stále přihlásit do počítače s Windows ve výchozím nastavení, včetně použití neomezeným prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27ab5-150">Remember that even an unprivileged user can still log into a Windows machine by default, including using unconstrained PowerShell.</span></span>
<span data-ttu-id="27ab5-151">Které umožní uživatelům procházet (část) systému souborů a další informace o prostředí operačního systému.</span><span class="sxs-lookup"><span data-stu-id="27ab5-151">That will allow them to browse (some of) the file system and learn more about your OS environment.</span></span>
<span data-ttu-id="27ab5-152">Zamknout Správce technologie Hyper-V jenom přístup k virtuálnímu počítači pomocí prostředí PowerShell přímo JEA, musíte se tak, aby odepřel práva místního přihlášení k účtu JEA Správce technologie Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="27ab5-152">To lock down a Hyper-V administrator to only access a VM using PowerShell Direct with JEA, you will need to deny local logon rights to the Hyper-V admin's JEA account.</span></span>