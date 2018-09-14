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
# <a name="using-jea"></a><span data-ttu-id="e54e8-103">Použití funkce JEA</span><span class="sxs-lookup"><span data-stu-id="e54e8-103">Using JEA</span></span>

> <span data-ttu-id="e54e8-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e54e8-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="e54e8-105">Toto téma popisuje různé způsoby se můžete připojit k a použití koncového bodu JEA.</span><span class="sxs-lookup"><span data-stu-id="e54e8-105">This topic describes the various ways you can connect to and use a JEA endpoint.</span></span>

## <a name="using-jea-interactively"></a><span data-ttu-id="e54e8-106">Použití interaktivní funkce JEA</span><span class="sxs-lookup"><span data-stu-id="e54e8-106">Using JEA interactively</span></span>

<span data-ttu-id="e54e8-107">Pokud testujete konfiguraci JEA nebo máte jednoduchých úloh pro uživatele k provedení, můžete použít JEA stejně jako byste to udělali regulární relaci vzdálené komunikace Powershellu.</span><span class="sxs-lookup"><span data-stu-id="e54e8-107">If you are testing your JEA configuration or have simple tasks for users to perform, you can use JEA the same way you would a regular PowerShell remoting session.</span></span>
<span data-ttu-id="e54e8-108">Pro úlohy komplexní vzdálené komunikace se doporučuje používat [implicitní vzdálené komunikace](#using-jea-with-implicit-remoting) místo aby bylo snazší pro vaše uživatele tím, že uživatelé pracovat s data objekty místně.</span><span class="sxs-lookup"><span data-stu-id="e54e8-108">For complex remoting tasks, it is recommended to use [implicit remoting](#using-jea-with-implicit-remoting) instead to make it easier for your users by allowing users to operate with the data objects locally.</span></span>

<span data-ttu-id="e54e8-109">Použití funkce JEA interaktivně, budete potřebovat:</span><span class="sxs-lookup"><span data-stu-id="e54e8-109">To use JEA interactively, you will need:</span></span>
- <span data-ttu-id="e54e8-110">Název počítače, které se připojujete (může být místní počítač)</span><span class="sxs-lookup"><span data-stu-id="e54e8-110">The name of the computer you are connecting to (can be the local machine)</span></span>
- <span data-ttu-id="e54e8-111">Název koncového bodu JEA registrován na tomto počítači</span><span class="sxs-lookup"><span data-stu-id="e54e8-111">The name of the JEA endpoint registered on that computer</span></span>
- <span data-ttu-id="e54e8-112">Přihlašovací údaje pro počítače, které mají přístup ke koncovému bodu JEA</span><span class="sxs-lookup"><span data-stu-id="e54e8-112">Credentials for the computer that have access to the JEA endpoint</span></span>

<span data-ttu-id="e54e8-113">Pomocí těchto informací v ručně, můžete začít používat relace JEA [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) nebo [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).</span><span class="sxs-lookup"><span data-stu-id="e54e8-113">With that information in hand, you can start a JEA session using [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) or [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).</span></span>

```powershell
$nonAdminCred = Get-Credential
Enter-PSSession -ComputerName localhost -ConfigurationName JEAMaintenance -Credential $nonAdminCred
```

<span data-ttu-id="e54e8-114">Pokud účet, jste aktuálně přihlášeni jako má přístup ke koncovému bodu JEA, můžete vynechat `-Credential` parametru.</span><span class="sxs-lookup"><span data-stu-id="e54e8-114">If the account you're currently logged in as has access to the JEA endpoint, you can omit the `-Credential` parameter.</span></span>

<span data-ttu-id="e54e8-115">Pokud PowerShell vyzve změny `[localhost]: PS>` budete vědět, že je nyní interakci s JEA relace.</span><span class="sxs-lookup"><span data-stu-id="e54e8-115">When the PowerShell prompt changes to `[localhost]: PS>` you will know that you are now interacting with the remote JEA session.</span></span>
<span data-ttu-id="e54e8-116">Můžete spustit `Get-Command` ke kontrole, které příkazy jsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="e54e8-116">You can run `Get-Command` to check which commands are available.</span></span>
<span data-ttu-id="e54e8-117">Musíte se obrátit se na správce a zjistěte, pokud existují nějaká omezení dostupné parametry nebo povolené parametr hodnoty.</span><span class="sxs-lookup"><span data-stu-id="e54e8-117">You will need to consult with your administrator to learn if there are any restrictions on the available parameters or allowable parameter values.</span></span>

<span data-ttu-id="e54e8-118">Připomínáme JEA relace pracovat v NoLanguage režimu, takže některé ze způsobů, jak obvykle použijete PowerShell nemusí být k dispozici.</span><span class="sxs-lookup"><span data-stu-id="e54e8-118">As a reminder, JEA sessions operate in NoLanguage mode, so some of the ways you typically use PowerShell may not be available.</span></span>
<span data-ttu-id="e54e8-119">Například nemůžete použít proměnné k ukládání dat nebo kontrole vlastností objektů vrácených z rutin.</span><span class="sxs-lookup"><span data-stu-id="e54e8-119">For instance, you cannot use variables to store data or inspect the properties on objects returned from cmdlets.</span></span>
<span data-ttu-id="e54e8-120">Následující příklad ukazuje příklad toho, jak využíváte prostředí PowerShell ještě dnes a dvou přístupů týkající se získání stejný příkaz funguje v režimu NoLanguage.</span><span class="sxs-lookup"><span data-stu-id="e54e8-120">The below example shows an example of how you may be using PowerShell today, and two approaches to get the same command working in NoLanguage mode.</span></span>

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

<span data-ttu-id="e54e8-121">Pro složitější vyvolání příkazu, kterým je tento přístup obtížné, zvažte použití [implicitní vzdálené komunikace](#using-jea-with-implicit-remoting) nebo [vytvoření vlastní funkce](role-capabilities.md#creating-custom-functions) zabalení, které vyžadujete funkce.</span><span class="sxs-lookup"><span data-stu-id="e54e8-121">For more complex command invocations that make this approach difficult, consider using [implicit remoting](#using-jea-with-implicit-remoting) or [creating custom functions](role-capabilities.md#creating-custom-functions) that wrap the functionality you desire.</span></span>

## <a name="using-jea-with-implicit-remoting"></a><span data-ttu-id="e54e8-122">Implicitní vzdálené komunikace pomocí funkce JEA</span><span class="sxs-lookup"><span data-stu-id="e54e8-122">Using JEA with implicit remoting</span></span>

<span data-ttu-id="e54e8-123">PowerShell podporuje model alternativní Vzdálená komunikace, ve kterém můžete importovat rutiny služby proxy ze vzdáleného počítače v místním počítači a s nimi pracovat, jako kdyby byly místní příkazy.</span><span class="sxs-lookup"><span data-stu-id="e54e8-123">PowerShell supports an alternative remoting model where you can import proxy cmdlets from a remote machine on your local computer and interact with them as if they were local commands.</span></span>
<span data-ttu-id="e54e8-124">To se označuje implicitní vzdálené komunikace a je vysvětlené také v [to *Hey, Scripting Guy!* blogový příspěvek](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).</span><span class="sxs-lookup"><span data-stu-id="e54e8-124">This is called implicit remoting, and is explained well in [this *Hey, Scripting Guy!* blog post](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).</span></span>
<span data-ttu-id="e54e8-125">Implicitní vzdálené komunikace je užitečné při práci s JEA, protože umožňuje pracovat s rutinami JEA v režimu úplné jazyka.</span><span class="sxs-lookup"><span data-stu-id="e54e8-125">Implicit remoting is particularly useful when working with JEA because it allows you to work with JEA cmdlets in a full language mode.</span></span>
<span data-ttu-id="e54e8-126">To znamená, že používají dokončování pomocí tabulátoru, proměnné, manipulovat s objekty a dokonce i pomocí místní skripty snadněji automatizovat proti koncového bodu JEA.</span><span class="sxs-lookup"><span data-stu-id="e54e8-126">This means you can use tab completion, variables, manipulate objects, and even use local scripts to more easily automate against a JEA endpoint.</span></span>
<span data-ttu-id="e54e8-127">Kdykoli můžete vyvolat příkaz proxy, data budou odeslány do koncového bodu JEA na vzdáleném počítači a spuštěny.</span><span class="sxs-lookup"><span data-stu-id="e54e8-127">Anytime you invoke a proxy command, the data will be sent to the JEA endpoint on the remote machine and executed there.</span></span>

<span data-ttu-id="e54e8-128">Implicitní vzdálené komunikace funguje tak, že rutiny Import z existující relace prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e54e8-128">Implicit remoting works by importing cmdlets from an existing PowerShell session.</span></span>
<span data-ttu-id="e54e8-129">Volitelně můžete jako předpona podstatná jména jednotlivých rutin proxy s řetězcem podle vašeho výběru k rozlišení, které příkazy jsou pro vzdálený systém.</span><span class="sxs-lookup"><span data-stu-id="e54e8-129">You can optionally choose to prefix the nouns of each proxy cmdlet with a string of your choosing to distinguish which commands are for the remote system.</span></span>
<span data-ttu-id="e54e8-130">Dočasný skript modulu, který obsahuje všechny příkazy proxy serveru se vytvoří a je možné po dobu trvání místní relaci Powershellu.</span><span class="sxs-lookup"><span data-stu-id="e54e8-130">A temporary script module containing all of the proxy commands will be created and can be used for the duration of your local PowerShell session.</span></span>

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Import the entire PSSession and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA'

# Invoke "Get-Command" on the remote JEA endpoint using the proxy cmdlet
Get-JEACommand
```

> [!IMPORTANT]
> <span data-ttu-id="e54e8-131">Některé systémy nemusí být možné naimportovat celou relaci JEA z důvodu omezení v rutinách JEA výchozí.</span><span class="sxs-lookup"><span data-stu-id="e54e8-131">Some systems may not be able to import an entire JEA session due to constraints in the default JEA cmdlets.</span></span>
> <span data-ttu-id="e54e8-132">Chcete-li se tomuto problému vyhnout, importovat pouze příkazy potřebné z relace JEA explicitně zadáním jejich názvy k `-CommandName` parametru.</span><span class="sxs-lookup"><span data-stu-id="e54e8-132">To get around this, only import the commands you need from the JEA session by explicitly providing their names to the `-CommandName` parameter.</span></span>
> <span data-ttu-id="e54e8-133">Budoucí aktualizace se řešení potíží s importem celý JEA debaty ohrožených systémech.</span><span class="sxs-lookup"><span data-stu-id="e54e8-133">A future update will address the issue with importing entire JEA sessions on affected systems.</span></span>

<span data-ttu-id="e54e8-134">Pokud nemůžete importovat JEA relace z důvodu omezení parametrů JEA výchozí, provedením následujících kroků, abyste odfiltrovat výchozí příkazy z importované sady.</span><span class="sxs-lookup"><span data-stu-id="e54e8-134">If you are unable to import a JEA session due to constraints on the default JEA parameters, you can follow the steps below to filter out the default commands from the imported set.</span></span>
<span data-ttu-id="e54e8-135">Stále budete moci používat příkazů, jako jsou `Select-Object` – použijete jen místní verze nainstalovaná v počítači, ne vzdálené relace JEA.</span><span class="sxs-lookup"><span data-stu-id="e54e8-135">You will still be able to use commands like `Select-Object` -- you'll just use the local version installed on your computer instead of the remote one in the JEA session.</span></span>

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

<span data-ttu-id="e54e8-136">Můžete také zachovat rutiny směrovány přes proxy server pomocí vzdálené komunikace implicitní [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).</span><span class="sxs-lookup"><span data-stu-id="e54e8-136">You can also persist the proxied cmdlets from implicit remoting using [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).</span></span>
<span data-ttu-id="e54e8-137">Další informace o implicitní vzdálenou komunikaci, najdete v dokumentaci nápovědy [Import-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) a [Import-Module](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/import-module).</span><span class="sxs-lookup"><span data-stu-id="e54e8-137">For more information about implicit remoting, check out the help documentation for [Import-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) and [Import-Module](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/import-module).</span></span>

## <a name="using-jea-programatically"></a><span data-ttu-id="e54e8-138">Programově pomocí funkce JEA</span><span class="sxs-lookup"><span data-stu-id="e54e8-138">Using JEA programatically</span></span>

<span data-ttu-id="e54e8-139">JEA je také možné automatizace systémů a uživatelské aplikace, jako je například interní pracovník aplikací a webů.</span><span class="sxs-lookup"><span data-stu-id="e54e8-139">JEA can also be used in automation systems and in user applications, such as in-house helpdesk apps and web sites.</span></span>
<span data-ttu-id="e54e8-140">Tento přístup je stejný jako, který k vytváření aplikací pro komunikaci s neomezeným koncových bodů prostředí PowerShell, s výstrahou, program měli vědět, že JEA je omezení příkazy, které lze spustit ve vzdálené relaci.</span><span class="sxs-lookup"><span data-stu-id="e54e8-140">The approach is the same as that for building apps that talk to unconstrained PowerShell endpoints, with the caveat that the program should be aware that JEA is limiting the commands that can be run in the remote session.</span></span>

<span data-ttu-id="e54e8-141">Pro jednoduché jednorázové úlohy, můžete použít [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command) ke spuštění sady příkazů pomocí JEA.</span><span class="sxs-lookup"><span data-stu-id="e54e8-141">For simple, one-off tasks, you can use [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command) to run a set of commands using JEA.</span></span>

```powershell
Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Process; Get-Service }
```

<span data-ttu-id="e54e8-142">Chcete-li zkontrolovat, které příkazy se dají používat, když se připojíte k relaci JEA, spusťte `Get-Command` a iterování přes výsledky ke kontrole povolených parametrů.</span><span class="sxs-lookup"><span data-stu-id="e54e8-142">To check which commands are available for use when you connect to a JEA session, run `Get-Command` and iterate through the results to check for the allowed parameters.</span></span>

```powershell
$allowedCommands = Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Command }
$allowedCommands | Where-Object { $_.CommandType -in 'Function', 'Cmdlet' } | Format-Table Name, Parameters
```

<span data-ttu-id="e54e8-143">Pokud vytváříte aplikaci C#, můžete vytvořit prostředí PowerShell prostředí runspace, který se připojuje k relaci JEA tak, že zadáte název konfigurace ve [WSManConnectionInfo](https://msdn.microsoft.com/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx) objektu.</span><span class="sxs-lookup"><span data-stu-id="e54e8-143">If you are building a C# app, you can create a PowerShell runspace that connects to a JEA session by specifying the configuration name in a [WSManConnectionInfo](https://msdn.microsoft.com/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx) object.</span></span>

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

## <a name="using-jea-with-powershell-direct"></a><span data-ttu-id="e54e8-144">Použití funkce JEA s přímou službu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e54e8-144">Using JEA with PowerShell Direct</span></span>

<span data-ttu-id="e54e8-145">Technologie Hyper-V ve Windows 10 a Windows Server 2016 nabízí [přímou službu PowerShell](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/vmsession), funkci, která umožňuje správci technologie Hyper-V ke správě virtuálních počítačů pomocí Powershellu bez ohledu na konfiguraci sítě nebo vzdálené správy nastavení na virtuálním počítači.</span><span class="sxs-lookup"><span data-stu-id="e54e8-145">Hyper-V in Windows 10 and Windows Server 2016 offers [PowerShell Direct](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/vmsession), a feature which allows Hyper-V administrators to manage virtual machines with PowerShell regardless of the network configuration or remote management settings on the virtual machine.</span></span>

<span data-ttu-id="e54e8-146">Přímou službu PowerShell můžete použít s JEA poskytnout přístup omezený Správce technologie Hyper-V k vašemu virtuálnímu počítači, což může být užitečné, pokud ztratit připojení k síti k vašemu virtuálnímu počítači a správce datového centra potřebný k opravě nastavení sítě.</span><span class="sxs-lookup"><span data-stu-id="e54e8-146">You can use PowerShell Direct with JEA to give a Hyper-V administrator limited access to your VM, which can be useful if you lose network connectivity to your VM and need a datacenter admin to fix the network settings.</span></span>

<span data-ttu-id="e54e8-147">Žádná další konfigurace je potřeba použít JEA přes přímou službu PowerShell, ale operační systém spuštěný ve virtuálním počítači musí být Windows 10 nebo Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="e54e8-147">No additional configuration is required to use JEA over PowerShell Direct, however the operating system running inside the virtual machine must be Windows 10 or Windows Server 2016.</span></span>
<span data-ttu-id="e54e8-148">Správce technologie Hyper-V může připojit ke koncovému bodu JEA pomocí `-VMName` nebo `-VMId` parametrů v rutinách PSRemoting:</span><span class="sxs-lookup"><span data-stu-id="e54e8-148">The Hyper-V admin can connect to the JEA endpoint by using the `-VMName` or `-VMId` parameters on PSRemoting cmdlets:</span></span>

```powershell
# Entering a JEA session using PowerShell Direct when the VM name is unique
Enter-PSSession -VMName 'SQL01' -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'

# Entering a JEA session using PowerShell Direct using VM ids
$vm = Get-VM -VMName 'MyVM' | Select-Object -First 1
Enter-PSSession -VMId $vm.VMId -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'
```

<span data-ttu-id="e54e8-149">Důrazně doporučujeme vytvořit jeden konkrétní uživatel místní s žádná jiná práva ke správě systému pro vaše Správce technologie Hyper-V použít.</span><span class="sxs-lookup"><span data-stu-id="e54e8-149">It is strongly recommended that you create a dedicated local user with no other rights to manage the system for your Hyper-V administrators to use.</span></span>
<span data-ttu-id="e54e8-150">Mějte na paměti, že jako Neprivilegovaný uživatel může stále přihlásit k počítači s Windows ve výchozím nastavení, včetně powershellu bez omezení.</span><span class="sxs-lookup"><span data-stu-id="e54e8-150">Remember that even an unprivileged user can still log into a Windows machine by default, including using unconstrained PowerShell.</span></span>
<span data-ttu-id="e54e8-151">Která umožní uživatelům procházet (některé z) v systému souborů a další informace o prostředí operačního systému.</span><span class="sxs-lookup"><span data-stu-id="e54e8-151">That will allow them to browse (some of) the file system and learn more about your OS environment.</span></span>
<span data-ttu-id="e54e8-152">Pro uzamčení správce technologie Hyper-V jenom přístup k virtuálnímu počítači pomocí funkce JEA přímou službu PowerShell, je potřeba zakázat místní přihlašovací práva pro účet JEA Správce technologie Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e54e8-152">To lock down a Hyper-V administrator to only access a VM using PowerShell Direct with JEA, you will need to deny local logon rights to the Hyper-V admin's JEA account.</span></span>