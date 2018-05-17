---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Ladění prostředků DSC
ms.openlocfilehash: 30d49768fc2301b5306d0001e157d60e2e991883
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="debugging-dsc-resources"></a>Ladění prostředků DSC

> Platí pro: Prostředí Windows PowerShell 5.0

V prostředí PowerShell 5.0 nová funkce byla zavedená v požadovaného stavu konfiguraci (DSC) umožňující ladění prostředek DSC podle konfigurace se právě používá.

## <a name="enabling-dsc-debugging"></a>Povolení ladění DSC
Než můžete ladit prostředek, je nutné povolit ladění voláním [povolit DscDebug](https://technet.microsoft.com/library/mt517870.aspx) rutiny.
Tato rutina provede povinný parametr **BreakAll**.

Můžete ověřit, že je pohledem na výsledek volání povoleno ladění [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx).

Následující výstup prostředí PowerShell zobrazuje výsledek povolení ladění:


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


## <a name="starting-a-configuration-with-debug-enabled"></a>Počáteční konfigurace s laděním povoleno
Chcete-li ladit prostředek DSC, začněte konfigurace, který volá tento prostředek.
V tomto příkladu podíváme jednoduché konfigurace, která volá [WindowsFeature](windowsfeatureResource.md) prostředek pro zkontrolujte, zda je nainstalován funkci "WindowsPowerShellWebAccess":

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
Po konfiguraci kompilování, spusťte ji pomocí volání [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx).
Konfigurace se zastaví, jakmile místní Configuration Manager (LCM) volání na první prostředek v konfiguraci.
Pokud použijete `-Verbose` a `-Wait` parametry, zobrazí výstup řádků je nutné zadat spustit ladění.

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
V tomto okamžiku LCM má názvem prostředku a se do první bod rozdělení.
Poslední tři řádky ve výstupu ukazují, jak připojit k procesu a spuštění ladění skriptu prostředků.

## <a name="debugging-the-resource-script"></a>Ladění skriptu prostředků

Spustí novou instanci třídy PowerShell ISE.
V podokně konzoly zadejte poslední tři řádky výstupu z `Start-DscConfiguration` jako příkazy, nahraďte výstupní `<credentials>` platné přihlašovací údaje.
Teď byste měli vidět řádku, který vypadá podobně jako:

```powershell
[TEST-SRV]: [DBG]: [Process:9000]: [RemoteHost]: PS C:\DebugTest>>
```

Skript prostředků se otevřou v podokně skriptu a ladicí program je zastavena na první řádek **Test TargetResource** – funkce ( **Test()** metoda na základě třídy prostředku).
Teď můžete příkazy ladění (ISE) v kroku prostřednictvím skriptu prostředků, podívejte se na hodnoty proměnné, prohlédnout zásobník volání a tak dále.
Informace o ladění v integrovaném Skriptovacím prostředí PowerShell najdete v tématu [postup ladění skriptů v systému Windows PowerShell ISE](https://technet.microsoft.com/en-us/library/dd819480.aspx).
Mějte na paměti, že každý řádek ve skriptu prostředků (nebo třída) je nastaven jako bod přerušení.

## <a name="disabling-dsc-debugging"></a>Zakázání ladění DSC

Po volání [povolit DscDebug](https://technet.microsoft.com/library/mt517870.aspx), všechna volání [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) bude mít za následek konfigurace rozdělení do ladicího programu. Povolit konfigurace, které normálně spustit, je nutné zakázat ladění voláním [zakázat DscDebug](https://technet.microsoft.com/en-us/library/mt517872.aspx) rutiny.

>**Poznámka:** Rebooting nezmění stav ladění LCM. Pokud je povoleno ladění, spouštění konfigurace bude stále přerušení ladicího po restartu systému.


## <a name="see-also"></a>Viz také
- [Psaní vlastních prostředků DSC s MOF](authoringResourceMOF.md)
- [Psaní vlastních prostředků DSC s třídami, prostředí PowerShell](authoringResourceClass.md)