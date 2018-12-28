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
# <a name="debugging-dsc-resources"></a>Ladění prostředků DSC

> Platí pro: Windows PowerShell 5.0

V Powershellu 5.0 nová funkce byla zavedena v požadovaného stavu konfiguraci (DSC), který umožňuje ladění prostředků DSC podle konfigurace se právě používá.

## <a name="enabling-dsc-debugging"></a>Povolení ladění DSC
Před prostředek lze ladit, je nutné povolit ladění pomocí volání [povolit DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug) rutiny.
Tato rutina použije povinný parametr **BreakAll**.

Můžete ověřit, že ladění bylo povoleno pohledem na výsledek volání [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager).

Následující výstup prostředí PowerShell ukazuje výsledek povolení ladění:


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


## <a name="starting-a-configuration-with-debug-enabled"></a>Počínaje konfiguraci ladění povoleno
Ladění prostředků DSC, spuštění konfigurace, který volá tento prostředek.
V tomto příkladu podíváme na jednoduchou konfiguraci, která volá **WindowsFeature** prostředků k zajištění, že je nainstalovaná funkce "WindowsPowerShellWebAccess":

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
Po kompilaci konfigurace, spusťte ji voláním [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration).
Konfigurace se zastaví, když místní Configuration Manageru (LCM) volá na první prostředek v konfiguraci.
Pokud používáte `-Verbose` a `-Wait` parametry, zobrazí výstup řádků, budete muset zadat pro spuštění ladění.

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
V tomto okamžiku má LCM názvem prostředku a přijdou do prvního bodu přerušení.
Poslední tři řádky ve výstupu ukazují, jak se připojit k procesu a spustit ladění skriptu prostředku.

## <a name="debugging-the-resource-script"></a>Ladění skriptu prostředků

Spusťte novou instanci třídy ISE Powershellu.
V podokně konzoly zadejte výstup z poslední tři řádky `Start-DscConfiguration` výstup příkazů nahraďte `<credentials>` platné přihlašovací údaje.
Teď byste měli vidět řádku, který vypadá podobně jako:

```powershell
[TEST-SRV]: [DBG]: [Process:9000]: [RemoteHost]: PS C:\DebugTest>>
```

Otevře se skript prostředků z podokna skriptu, a ladicí program je zastavený na první řádek **testovací TargetResource** – funkce ( **Test()** metody založené na třídě prostředku).
Nyní můžete ladicími příkazy v prostředí ISE krokovat skript prostředků, podívejte se na hodnoty proměnných, zobrazení zásobníku volání a tak dále. Mějte na paměti, že každý řádek ve skriptu prostředků (nebo třídy) je nastaven jako přerušení.

## <a name="disabling-dsc-debugging"></a>Zakázání ladění DSC

Po volání [povolit DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug), všechna volání [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) způsobí konfigurace dopadem na dřívější kód do ladicího programu. Povolit konfigurace umožnili normální spuštění, je nutné zakázat ladění pomocí volání [zakázat DscDebug](/powershell/module/PSDesiredStateConfiguration/Disable-DscDebug) rutiny.

>**Poznámka:** Restartování ladění stavu LCM nezmění. Pokud je povoleno ladění, spouští se konfigurace se i přesto narušit funkce do ladicího programu po restartu.

## <a name="see-also"></a>Viz také

- [Psaní vlastních prostředků DSC s MOF](../resources/authoringResourceMOF.md)
- [Psaní vlastních prostředků DSC pomocí tříd Powershellu](../resources/authoringResourceClass.md)
