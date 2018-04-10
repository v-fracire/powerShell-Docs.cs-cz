---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Ladění prostředků DSC
ms.openlocfilehash: 6a1f4b04a11185c2cfe9be26324bd66ed13ca7dd
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="debugging-dsc-resources"></a><span data-ttu-id="cd64a-103">Ladění prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="cd64a-103">Debugging DSC resources</span></span>

> <span data-ttu-id="cd64a-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="cd64a-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="cd64a-105">V prostředí PowerShell 5.0 nová funkce byla zavedená v požadovaného stavu konfiguraci (DSC) umožňující ladění prostředek DSC podle konfigurace se právě používá.</span><span class="sxs-lookup"><span data-stu-id="cd64a-105">In PowerShell 5.0, a new feature was introduced in Desired State Configuraiton (DSC) that allows you to debug a DSC resource as a configuration is being applied.</span></span>

## <a name="enabling-dsc-debugging"></a><span data-ttu-id="cd64a-106">Povolení ladění DSC</span><span class="sxs-lookup"><span data-stu-id="cd64a-106">Enabling DSC debugging</span></span>
<span data-ttu-id="cd64a-107">Než můžete ladit prostředek, je nutné povolit ladění voláním [povolit DscDebug](https://technet.microsoft.com/library/mt517870.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="cd64a-107">Before you can debug a resource, you have to enable debugging by calling the [Enable-DscDebug](https://technet.microsoft.com/library/mt517870.aspx) cmdlet.</span></span>
<span data-ttu-id="cd64a-108">Tato rutina provede povinný parametr **BreakAll**.</span><span class="sxs-lookup"><span data-stu-id="cd64a-108">This cmdlet takes a mandatory parameter, **BreakAll**.</span></span>

<span data-ttu-id="cd64a-109">Můžete ověřit, že je pohledem na výsledek volání povoleno ladění [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd64a-109">You can verify that debugging has been enabled by looking at the result of a call to [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx).</span></span>

<span data-ttu-id="cd64a-110">Následující výstup prostředí PowerShell zobrazuje výsledek povolení ladění:</span><span class="sxs-lookup"><span data-stu-id="cd64a-110">The following PowerShell output shows the result of enabling debugging:</span></span>


```powershell
PS C:\DebugTest> $LCM = Get-DscLocalConfigurationManager

PS C:\DebugTest> $LCM.DebugMode
NONE

PS C:\DebugTest> Enable-DscDebug -BreakAll

PS C:\DebugTest> $LCM = Get-DscLocalConfigurationManager

PS C:\DebugTest> $LCM.DebugMode
ForceModuleImport
ResourceScriptBreakAll

PS C:\DebugTest>
```


## <a name="starting-a-configuration-with-debug-enabled"></a><span data-ttu-id="cd64a-111">Počáteční konfigurace s laděním povoleno</span><span class="sxs-lookup"><span data-stu-id="cd64a-111">Starting a configuration with debug enabled</span></span>
<span data-ttu-id="cd64a-112">Chcete-li ladit prostředek DSC, začněte konfigurace, který volá tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="cd64a-112">To debug a DSC resource, you start a configuration that calls that resource.</span></span>
<span data-ttu-id="cd64a-113">V tomto příkladu podíváme jednoduché konfigurace, která volá [WindowsFeature](windowsfeatureResource.md) prostředek pro zkontrolujte, zda je nainstalován funkci "WindowsPowerShellWebAccess":</span><span class="sxs-lookup"><span data-stu-id="cd64a-113">For this example, we'll look at a simple configuration that calls the [WindowsFeature](windowsfeatureResource.md) resource to ensure that the "WindowsPowerShellWebAccess" feature is installed:</span></span>

```powershell
Configuration PSWebAccess
    {
    Import-DscResource -ModuleName 'PsDesiredStateConfiguration'
    Node localhost
        {
        WindowsFeature PSWA
            {
            Name = 'WindowsPowerShellWebAccess'
            Ensure = 'Present'
            }
        }
    }
PSWebAccess
```
<span data-ttu-id="cd64a-114">Po konfiguraci kompilování, spusťte ji pomocí volání [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd64a-114">After compiling the configuration, start it by calling [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx).</span></span>
<span data-ttu-id="cd64a-115">Konfigurace se zastaví, jakmile místní Configuration Manager (LCM) volání na první prostředek v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="cd64a-115">The configuration will stop when the Local Configuration Manager (LCM) calls into the first resource in the configuration.</span></span>
<span data-ttu-id="cd64a-116">Pokud použijete `-Verbose` a `-Wait` parametry, zobrazí výstup řádků je nutné zadat spustit ladění.</span><span class="sxs-lookup"><span data-stu-id="cd64a-116">If you use the `-Verbose` and `-Wait` parameters, the output displays the lines you need to enter to start debugging.</span></span>

```powershell
Start-DscConfiguration .\PSWebAccess -Wait -Verbose
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' = SendConfigurationApply,'className' = MSFT_DSCLocalConfiguration
Manager,'namespaceName' = root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer TEST-SRV with user sid S-1-5-21-2127521184-1604012920-1887927527-108583.
VERBOSE: An LCM method call arrived from computer TEST-SRV with user sid S-1-5-21-2127521184-1604012920-1887927527-108583.
VERBOSE: [TEST-SRV]: LCM:  [ Start  Set      ]
WARNING: [TEST-SRV]:                            [DSCEngine] Warning LCM is in Debug 'ResourceScriptBreakAll' mode.  Resource script processing will
be stopped to wait for PowerShell script debugger to attach.
VERBOSE: [TEST-SRV]:                            [DSCEngine] Importing the module C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateCo
nfiguration\DscResources\MSFT_RoleResource\MSFT_RoleResource.psm1 in force mode.
VERBOSE: [TEST-SRV]: LCM:  [ Start  Resource ]  [[WindowsFeature]PSWA]
VERBOSE: [TEST-SRV]: LCM:  [ Start  Test     ]  [[WindowsFeature]PSWA]
VERBOSE: [TEST-SRV]:                            [[WindowsFeature]PSWA] Importing the module MSFT_RoleResource in force mode.
WARNING: [TEST-SRV]:                            [[WindowsFeature]PSWA] Resource is waiting for PowerShell script debugger to attach.
Use the following commands to begin debugging this resource script:
Enter-PSSession -ComputerName TEST-SRV -Credential <credentials>
Enter-PSHostProcess -Id 9000 -AppDomainName DscPsPluginWkr_AppDomain
Debug-Runspace -Id 9
```
<span data-ttu-id="cd64a-117">V tomto okamžiku LCM má názvem prostředku a se do první bod rozdělení.</span><span class="sxs-lookup"><span data-stu-id="cd64a-117">At this point, the LCM has called the resource, and come to the first break point.</span></span>
<span data-ttu-id="cd64a-118">Poslední tři řádky ve výstupu ukazují, jak připojit k procesu a spuštění ladění skriptu prostředků.</span><span class="sxs-lookup"><span data-stu-id="cd64a-118">The last three lines in the output show you how to attach to the process and start debugging the resource script.</span></span>

## <a name="debugging-the-resource-script"></a><span data-ttu-id="cd64a-119">Ladění skriptu prostředků</span><span class="sxs-lookup"><span data-stu-id="cd64a-119">Debugging the resource script</span></span>

<span data-ttu-id="cd64a-120">Spustí novou instanci třídy PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="cd64a-120">Start a new instance of the PowerShell ISE.</span></span>
<span data-ttu-id="cd64a-121">V podokně konzoly zadejte poslední tři řádky výstupu z `Start-DscConfiguration` jako příkazy, nahraďte výstupní `<credentials>` platné přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="cd64a-121">In the console pane, enter the last three lines of output from the `Start-DscConfiguration` output as commands, replacing `<credentials>` with valid user credentials.</span></span>
<span data-ttu-id="cd64a-122">Teď byste měli vidět řádku, který vypadá podobně jako:</span><span class="sxs-lookup"><span data-stu-id="cd64a-122">You should now see a prompt that looks similar to:</span></span>

```powershell
[TEST-SRV]: [DBG]: [Process:9000]: [RemoteHost]: PS C:\DebugTest>>
```

<span data-ttu-id="cd64a-123">Skript prostředků se otevřou v podokně skriptu a ladicí program je zastavena na první řádek **Test TargetResource** – funkce ( **Test()** metoda na základě třídy prostředku).</span><span class="sxs-lookup"><span data-stu-id="cd64a-123">The resource script will open in the script pane, and the debugger is stopped at the first line of the **Test-TargetResource** function (the **Test()** method of a class-based resource).</span></span>
<span data-ttu-id="cd64a-124">Teď můžete příkazy ladění (ISE) v kroku prostřednictvím skriptu prostředků, podívejte se na hodnoty proměnné, prohlédnout zásobník volání a tak dále.</span><span class="sxs-lookup"><span data-stu-id="cd64a-124">Now you can use the debug commands in the ISE to step through the resource script, look at variable values, view the call stack, and so on.</span></span>
<span data-ttu-id="cd64a-125">Informace o ladění v integrovaném Skriptovacím prostředí PowerShell najdete v tématu [postup ladění skriptů v systému Windows PowerShell ISE](https://technet.microsoft.com/en-us/library/dd819480.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd64a-125">For information about debugging in the PowerShell ISE, see [How to Debug Scripts in Windows PowerShell ISE](https://technet.microsoft.com/en-us/library/dd819480.aspx).</span></span>
<span data-ttu-id="cd64a-126">Mějte na paměti, že každý řádek ve skriptu prostředků (nebo třída) je nastaven jako bod přerušení.</span><span class="sxs-lookup"><span data-stu-id="cd64a-126">Remember that every line in the resource script (or class) is set as a break point.</span></span>

## <a name="disabling-dsc-debugging"></a><span data-ttu-id="cd64a-127">Zakázání ladění DSC</span><span class="sxs-lookup"><span data-stu-id="cd64a-127">Disabling DSC debugging</span></span>

<span data-ttu-id="cd64a-128">Po volání [povolit DscDebug](https://technet.microsoft.com/library/mt517870.aspx), všechna volání [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) bude mít za následek konfigurace rozdělení do ladicího programu.</span><span class="sxs-lookup"><span data-stu-id="cd64a-128">After calling [Enable-DscDebug](https://technet.microsoft.com/library/mt517870.aspx), all calls to [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) will result in the configuration breaking into the debugger.</span></span> <span data-ttu-id="cd64a-129">Povolit konfigurace, které normálně spustit, je nutné zakázat ladění voláním [zakázat DscDebug](https://technet.microsoft.com/en-us/library/mt517872.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="cd64a-129">To allow configurations to run normally, you must disable debugging by calling the [Disable-DscDebug](https://technet.microsoft.com/en-us/library/mt517872.aspx) cmdlet.</span></span>

><span data-ttu-id="cd64a-130">**Poznámka:** Rebooting nezmění stav ladění LCM.</span><span class="sxs-lookup"><span data-stu-id="cd64a-130">**Note:** Rebooting does not change the debug state of the LCM.</span></span> <span data-ttu-id="cd64a-131">Pokud je povoleno ladění, spouštění konfigurace bude stále přerušení ladicího po restartu systému.</span><span class="sxs-lookup"><span data-stu-id="cd64a-131">If debugging is enabled, starting a configuration will still break into the debugger after a reboot.</span></span>


## <a name="see-also"></a><span data-ttu-id="cd64a-132">Viz také</span><span class="sxs-lookup"><span data-stu-id="cd64a-132">See Also</span></span>
- [<span data-ttu-id="cd64a-133">Psaní vlastních prostředků DSC s MOF</span><span class="sxs-lookup"><span data-stu-id="cd64a-133">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
- [<span data-ttu-id="cd64a-134">Psaní vlastních prostředků DSC s třídami, prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd64a-134">Writing a custom DSC resource with PowerShell classes</span></span>](authoringResourceClass.md)