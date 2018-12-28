---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Ladění prostředků DSC
ms.openlocfilehash: 9b2e7dd9b42332b869c4d7fabb21bd4b5a6b8800
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403714"
---
# <a name="debugging-dsc-resources"></a><span data-ttu-id="ddea5-103">Ladění prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="ddea5-103">Debugging DSC resources</span></span>

> <span data-ttu-id="ddea5-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="ddea5-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="ddea5-105">V Powershellu 5.0 nová funkce byla zavedena v požadovaného stavu konfiguraci (DSC), který umožňuje ladění prostředků DSC podle konfigurace se právě používá.</span><span class="sxs-lookup"><span data-stu-id="ddea5-105">In PowerShell 5.0, a new feature was introduced in Desired State Configuraiton (DSC) that allows you to debug a DSC resource as a configuration is being applied.</span></span>

## <a name="enabling-dsc-debugging"></a><span data-ttu-id="ddea5-106">Povolení ladění DSC</span><span class="sxs-lookup"><span data-stu-id="ddea5-106">Enabling DSC debugging</span></span>
<span data-ttu-id="ddea5-107">Před prostředek lze ladit, je nutné povolit ladění pomocí volání [povolit DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug) rutiny.</span><span class="sxs-lookup"><span data-stu-id="ddea5-107">Before you can debug a resource, you have to enable debugging by calling the [Enable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug) cmdlet.</span></span>
<span data-ttu-id="ddea5-108">Tato rutina použije povinný parametr **BreakAll**.</span><span class="sxs-lookup"><span data-stu-id="ddea5-108">This cmdlet takes a mandatory parameter, **BreakAll**.</span></span>

<span data-ttu-id="ddea5-109">Můžete ověřit, že ladění bylo povoleno pohledem na výsledek volání [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager).</span><span class="sxs-lookup"><span data-stu-id="ddea5-109">You can verify that debugging has been enabled by looking at the result of a call to [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager).</span></span>

<span data-ttu-id="ddea5-110">Následující výstup prostředí PowerShell ukazuje výsledek povolení ladění:</span><span class="sxs-lookup"><span data-stu-id="ddea5-110">The following PowerShell output shows the result of enabling debugging:</span></span>


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


## <a name="starting-a-configuration-with-debug-enabled"></a><span data-ttu-id="ddea5-111">Počínaje konfiguraci ladění povoleno</span><span class="sxs-lookup"><span data-stu-id="ddea5-111">Starting a configuration with debug enabled</span></span>
<span data-ttu-id="ddea5-112">Ladění prostředků DSC, spuštění konfigurace, který volá tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="ddea5-112">To debug a DSC resource, you start a configuration that calls that resource.</span></span>
<span data-ttu-id="ddea5-113">V tomto příkladu podíváme na jednoduchou konfiguraci, která volá **WindowsFeature** prostředků k zajištění, že je nainstalovaná funkce "WindowsPowerShellWebAccess":</span><span class="sxs-lookup"><span data-stu-id="ddea5-113">For this example, we'll look at a simple configuration that calls the **WindowsFeature** resource to ensure that the "WindowsPowerShellWebAccess" feature is installed:</span></span>

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
<span data-ttu-id="ddea5-114">Po kompilaci konfigurace, spusťte ji voláním [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration).</span><span class="sxs-lookup"><span data-stu-id="ddea5-114">After compiling the configuration, start it by calling [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration).</span></span>
<span data-ttu-id="ddea5-115">Konfigurace se zastaví, když místní Configuration Manageru (LCM) volá na první prostředek v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="ddea5-115">The configuration will stop when the Local Configuration Manager (LCM) calls into the first resource in the configuration.</span></span>
<span data-ttu-id="ddea5-116">Pokud používáte `-Verbose` a `-Wait` parametry, zobrazí výstup řádků, budete muset zadat pro spuštění ladění.</span><span class="sxs-lookup"><span data-stu-id="ddea5-116">If you use the `-Verbose` and `-Wait` parameters, the output displays the lines you need to enter to start debugging.</span></span>

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
<span data-ttu-id="ddea5-117">V tomto okamžiku má LCM názvem prostředku a přijdou do prvního bodu přerušení.</span><span class="sxs-lookup"><span data-stu-id="ddea5-117">At this point, the LCM has called the resource, and come to the first break point.</span></span>
<span data-ttu-id="ddea5-118">Poslední tři řádky ve výstupu ukazují, jak se připojit k procesu a spustit ladění skriptu prostředku.</span><span class="sxs-lookup"><span data-stu-id="ddea5-118">The last three lines in the output show you how to attach to the process and start debugging the resource script.</span></span>

## <a name="debugging-the-resource-script"></a><span data-ttu-id="ddea5-119">Ladění skriptu prostředků</span><span class="sxs-lookup"><span data-stu-id="ddea5-119">Debugging the resource script</span></span>

<span data-ttu-id="ddea5-120">Spusťte novou instanci třídy ISE Powershellu.</span><span class="sxs-lookup"><span data-stu-id="ddea5-120">Start a new instance of the PowerShell ISE.</span></span>
<span data-ttu-id="ddea5-121">V podokně konzoly zadejte výstup z poslední tři řádky `Start-DscConfiguration` výstup příkazů nahraďte `<credentials>` platné přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="ddea5-121">In the console pane, enter the last three lines of output from the `Start-DscConfiguration` output as commands, replacing `<credentials>` with valid user credentials.</span></span>
<span data-ttu-id="ddea5-122">Teď byste měli vidět řádku, který vypadá podobně jako:</span><span class="sxs-lookup"><span data-stu-id="ddea5-122">You should now see a prompt that looks similar to:</span></span>

```powershell
[TEST-SRV]: [DBG]: [Process:9000]: [RemoteHost]: PS C:\DebugTest>>
```

<span data-ttu-id="ddea5-123">Otevře se skript prostředků z podokna skriptu, a ladicí program je zastavený na první řádek **testovací TargetResource** – funkce ( **Test()** metody založené na třídě prostředku).</span><span class="sxs-lookup"><span data-stu-id="ddea5-123">The resource script will open in the script pane, and the debugger is stopped at the first line of the **Test-TargetResource** function (the **Test()** method of a class-based resource).</span></span>
<span data-ttu-id="ddea5-124">Nyní můžete ladicími příkazy v prostředí ISE krokovat skript prostředků, podívejte se na hodnoty proměnných, zobrazení zásobníku volání a tak dále.</span><span class="sxs-lookup"><span data-stu-id="ddea5-124">Now you can use the debug commands in the ISE to step through the resource script, look at variable values, view the call stack, and so on.</span></span> <span data-ttu-id="ddea5-125">Mějte na paměti, že každý řádek ve skriptu prostředků (nebo třídy) je nastaven jako přerušení.</span><span class="sxs-lookup"><span data-stu-id="ddea5-125">Remember that every line in the resource script (or class) is set as a break point.</span></span>

## <a name="disabling-dsc-debugging"></a><span data-ttu-id="ddea5-126">Zakázání ladění DSC</span><span class="sxs-lookup"><span data-stu-id="ddea5-126">Disabling DSC debugging</span></span>

<span data-ttu-id="ddea5-127">Po volání [povolit DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug), všechna volání [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) způsobí konfigurace dopadem na dřívější kód do ladicího programu.</span><span class="sxs-lookup"><span data-stu-id="ddea5-127">After calling [Enable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug), all calls to [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) will result in the configuration breaking into the debugger.</span></span> <span data-ttu-id="ddea5-128">Povolit konfigurace umožnili normální spuštění, je nutné zakázat ladění pomocí volání [zakázat DscDebug](/powershell/module/PSDesiredStateConfiguration/Disable-DscDebug) rutiny.</span><span class="sxs-lookup"><span data-stu-id="ddea5-128">To allow configurations to run normally, you must disable debugging by calling the [Disable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Disable-DscDebug) cmdlet.</span></span>

><span data-ttu-id="ddea5-129">**Poznámka:** Restartování ladění stavu LCM nezmění.</span><span class="sxs-lookup"><span data-stu-id="ddea5-129">**Note:** Rebooting does not change the debug state of the LCM.</span></span> <span data-ttu-id="ddea5-130">Pokud je povoleno ladění, spouští se konfigurace se i přesto narušit funkce do ladicího programu po restartu.</span><span class="sxs-lookup"><span data-stu-id="ddea5-130">If debugging is enabled, starting a configuration will still break into the debugger after a reboot.</span></span>

## <a name="see-also"></a><span data-ttu-id="ddea5-131">Viz také</span><span class="sxs-lookup"><span data-stu-id="ddea5-131">See Also</span></span>

- [<span data-ttu-id="ddea5-132">Psaní vlastních prostředků DSC s MOF</span><span class="sxs-lookup"><span data-stu-id="ddea5-132">Writing a custom DSC resource with MOF</span></span>](../resources/authoringResourceMOF.md)
- [<span data-ttu-id="ddea5-133">Psaní vlastních prostředků DSC pomocí tříd Powershellu</span><span class="sxs-lookup"><span data-stu-id="ddea5-133">Writing a custom DSC resource with PowerShell classes</span></span>](../resources/authoringResourceClass.md)
