---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Řešení potíží s DSC"
ms.openlocfilehash: cdb11a80daecec0e0d01071752612663ac69ac6d
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-dsc"></a>Řešení potíží s DSC

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Toto téma popisuje způsoby řešení DSC, když vzniknou problémy.

## <a name="winrm-dependency"></a>WinRM závislostí

Požadovaného stavu aplikace Windows PowerShell (DSC) závisí na vzdálené správy systému Windows. WinRM není povoleno ve výchozím nastavení na Windows Server 2008 R2 a Windows 7. Spustit ```Set-WSManQuickConfig```, v prostředí Windows PowerShell se zvýšenými oprávněními relace, aby Služba WinRM.

## <a name="using-get-dscconfigurationstatus"></a>Pomocí Get-DscConfigurationStatus

[Get-DscConfigurationStatus](https://technet.microsoft.com/library/mt517868.aspx) rutiny získá informace o konfiguraci stavu z cílového uzlu. Bohaté objektu se vrátí, který obsahuje souhrnné informace o tom, jestli spuštění konfigurace byla úspěšná. Můžete můžete proniknout do objektu, který chcete zjistit podrobnosti o konfiguraci, spuštění například:

* Všechny prostředky, které se nezdařilo
* Jakémukoli prostředku, který požadovaný restart
* Spustit meta-konfigurační nastavení v době konfigurace
* Atd.

Následující sada parametrů vrátí informace o stavu pro poslední konfigurace spustit:

```powershell
Get-DscConfigurationStatus  [-CimSession <CimSession[]>] 
                            [-ThrottleLimit <int>] 
                            [-AsJob] 
                            [<CommonParameters>]
```
Následující sada parametrů vrátí informace o stavu pro všechny předchozí konfigurace spustí:

```powershell
Get-DscConfigurationStatus  -All 
                            [-CimSession <CimSession[]>] 
                            [-ThrottleLimit <int>] 
                            [-AsJob] 
                            [<CommonParameters>]
```

## <a name="example"></a>Příklad

```powershell
PS C:\> $Status = Get-DscConfigurationStatus 

PS C:\> $Status

Status      StartDate               Type            Mode    RebootRequested     NumberOfResources
------      ---------               ----            ----    ---------------     -----------------
Failure     11/24/2015  3:44:56     Consistency     Push    True                36

PS C:\> $Status.ResourcesNotInDesiredState

ConfigurationName       :   MyService
DependsOn               :   
ModuleName              :   PSDesiredStateConfiguration
ModuleVersion           :   1.1
PsDscRunAsCredential    :   
ResourceID              :   [File]ServiceDll
SourceInfo              :   c:\git\CustomerService\Configs\MyCustomService.ps1::5::34::File
DurationInSeconds       :   0.19
Error                   :   SourcePath must be accessible for current configuration. The related file/directory is:
                            \\Server93\Shared\contosoApp.dll. The related ResourceID is [File]ServiceDll
FinalState              :   
InDesiredState          :   False
InitialState            :   
InstanceName            :   ServiceDll
RebootRequested         :   False
ReosurceName            :   File
StartDate               :   11/24/2015  3:44:56
PSComputerName          :
```

## <a name="my-script-wont-run-using-dsc-logs-to-diagnose-script-errors"></a>Moje skript nespustí: pomocí DSC protokoly a diagnostikovat chyby skriptu

Veškerý software Windows, jako je DSC zaznamenává chyby a události v [protokoly](https://msdn.microsoft.com/library/windows/desktop/aa363632.aspx) , si můžete prohlížet [Prohlížeč událostí](http://windows.microsoft.com/windows/what-information-event-logs-event-viewer). Zkoumání tyto protokoly pomůžou pochopit, proč konkrétní operace se nezdařila a jak v budoucnu nedošlo k selhání. Psaní konfiguračních skriptů může být složité, takže k usnadnění sledování chyb jako autor můžete, použijte prostředek DSC protokolu sledovat postup konfigurace DSC analytické protokolu událostí.

## <a name="where-are-dsc-event-logs"></a>Kde jsou protokoly událostí DSC?

V prohlížeči událostí, jsou události DSC v: **aplikací a konfigurace služeb Logs/Microsoft/Windows/žádaný stavu**

Odpovídajících rutin prostředí PowerShell, [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx), lze také spustit a zobrazit protokoly událostí:

```
PS C:\> Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
   ProviderName: Microsoft-Windows-DSC
TimeCreated                     Id LevelDisplayName Message                                                                                                  
-----------                     -- ---------------- -------                                                                                                  
11/17/2014 10:27:23 PM        4102 Information      Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} : 
```

Jako v příkladu nahoře, je název primární protokolu DSC **Microsoft -> Windows -> DSC** (jiné názvy protokolu v části Windows nezobrazují zde jako stručný výtah). Název primárního se připojuje k název kanálu pro vytvoření názvu celý protokol. Modul DSC zapíše především na tři typy protokolů: [funkčnosti, analýzu a ladit protokoly](https://technet.microsoft.com/library/cc722404.aspx). Od analytické a ladicí protokoly jsou ve výchozím nastavení vypnuté, měli byste povolit v prohlížeči událostí. Chcete-li to provést, otevřete Prohlížeč událostí zadáním EventLog zobrazit v prostředí Windows PowerShell; nebo klikněte na tlačítko **spustit** tlačítko, klikněte na tlačítko **ovládací panely**, klikněte na tlačítko **nástroje pro správu**a potom klikněte na **Prohlížeč událostí**. Na **zobrazení** nabídky v prohlížeči událostí, klikněte na tlačítko **zobrazit protokoly pro ladění a**. Název protokolu pro analytické kanál je **Microsoft-Windows-Dsc/analytické**, a je ladění kanál **Microsoft-Windows-Dsc/Debug**. Můžete také použít [wevtutil](https://technet.microsoft.com/library/cc732848.aspx) nástroj umožňující protokoly, jak je znázorněno v následujícím příkladu.

```powershell
wevtutil.exe set-log “Microsoft-Windows-Dsc/Analytic” /q:true /e:true
```

## <a name="what-do-dsc-logs-contain"></a>Co DSC protokoly obsahovat?

DSC protokoly jsou rozděleny přes tři kanály protokolů založen na významu zprávy. Operační protokol v DSC obsahuje všechny chybové zprávy a slouží k identifikaci problém. Analytické protokolu má vyšší objem událostí a můžete zjistit, kde došlo k chybám. Tento kanál obsahuje taky podrobné zprávy (pokud existuje). Ladění protokolu obsahuje protokoly, které vám může pomoct pochopit, jak došlo k chybě. Zprávy o událostech DSC jsou strukturovaná tak, aby každý zpráva události začíná ID úlohy, který jedinečně reprezentuje operaci DSC. Následující příklad se pokusí získat zprávy z první událost se zaznamená do operační protokol DSC.

```powershell
PS C:\> $AllDscOpEvents = Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
PS C:\> $FirstOperationalEvent = $AllDscOpEvents[0]
PS C:\> $FirstOperationalEvent.Message
Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} : 
Consistency engine was run successfully. 
```

DSC události jsou protokolovány v konkrétní strukturu, která umožňuje uživateli pro agregaci událostí z jedné úlohy DSC. Struktura je následující:

**ID úlohy: <Guid>**
**<Event Message>**

## <a name="gathering-events-from-a-single-dsc-operation"></a>Shromažďování událostí z jedné operace DSC

Protokoly událostí DSC obsahovat události vygenerované pomocí různých operací DSC. Však obvykle budete nevadí podrobností o jenom jeden konkrétní operaci. Všechny protokoly DSC lze seskupovat podle vlastnost ID úlohy, které jsou jedinečné pro každé operace DSC. ID úlohy se zobrazí jako první hodnoty vlastností v všechny události DSC. Následující kroky popisují, jak shromažďování všech událostí ve struktuře seskupené pole.

```powershell
<##########################################################################
 Step 1 : Enable analytic and debug DSC channels (Operational channel is enabled by default)
###########################################################################>
 
wevtutil.exe set-log “Microsoft-Windows-Dsc/Analytic” /q:true /e:true
wevtutil.exe set-log “Microsoft-Windows-Dsc/Debug” /q:True /e:true
 
<##########################################################################
 Step 2 : Perform the required DSC operation (Below is an example, you could run any DSC operation instead)
###########################################################################>
 
Get-DscLocalConfigurationManager
 
<##########################################################################
Step 3 : Collect all DSC Logs, from the Analytic, Debug and Operational channels
###########################################################################>
 
$DscEvents=[System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Operational") `
         + [System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Analytic" -Oldest) `
         + [System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Debug" -Oldest)
 
 
<##########################################################################
 Step 4 : Group all logs based on the job ID
###########################################################################>
$SeparateDscOperations = $DscEvents | Group {$_.Properties[0].value}  
```

Tady, proměnná `$SeparateDscOperations` obsahuje protokoly seskupené podle ID úloh. Každý element pole Tato proměnná představuje skupinu události zapsané podle jiné operace DSC, povolení přístupu k další informace o protokoly.

```
PS C:\> $SeparateDscOperations
 
Count Name                      Group                                                                     
----- ----                      -----                                                                     
   48 {1A776B6A-5BAC-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
   40 {E557E999-5BA8-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
PS C:\> $SeparateDscOperations[0].Group
   ProviderName: Microsoft-Windows-DSC
TimeCreated                     Id LevelDisplayName Message                                               
-----------                     -- ---------------- -------                                               
12/2/2013 3:47:29 PM          4115 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4198 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4114 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4102 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4098 Warning          Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4098 Warning          Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4176 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...       
```

Můžete rozbalit data v proměnné `$SeparateDscOperations` pomocí [Where-Object](https://technet.microsoft.com/library/ee177028.aspx). Následují pět scénáře, ve kterých můžete chtít extrahovat data pro řešení potíží s DSC:

### <a name="1-operations-failures"></a>1: selhání operací

Všechny události mít [úrovně závažnosti](https://msdn.microsoft.com/library/dd996917(v=vs.85)). Tyto informace slouží k identifikaci chybové události:

```
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.LevelDisplayName -contains "Error"}
Count Name                      Group                                                                     
----- ----                      -----                                                                     
   38 {5BCA8BE7-5BB6-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
```

### <a name="2-details-of-operations-run-in-the-last-half-hour"></a>2: spuštění podrobnosti operace v poslední půl hodiny

`TimeCreated`, v době vytvoření události stavy vlastnost každé události systému Windows. Porovnání tato vlastnost s objektem konkrétní datum a čas mohou být použity k filtrování všechny události:

```powershell
PS C:\> $DateLatest = (Get-Date).AddMinutes(-30)
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.TimeCreated -gt $DateLatest}
Count Name                      Group                                                                     
----- ----                      -----                                                                     
    1 {6CEC5B09-5BB0-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord}   
```

### <a name="3-messages-from-the-latest-operation"></a>3: zprávy z nejnovější operace

Poslední operaci je uložen v první index pole skupiny `$SeparateDscOperations`. Dotazování skupiny zprávy pro index 0 vrátí všechny zprávy nejnovější operace:

```powershelll
PS C:\> $SeparateDscOperations[0].Group.Message
Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} : 
Running consistency engine.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : 
Configuration is sent from computer NULL by user sid S-1-5-18.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : 
Displaying messages from built-in DSC resources:
 WMI channel 1 
 ResourceID:  
 Message : [INCH-VM]:                            [] Starting consistency engine.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : 
Displaying messages from built-in DSC resources:
 WMI channel 1 
 ResourceID:  
 Message : [INCH-VM]:                            [] Consistency check completed. 
```

### <a name="4-error-messages-logged-for-recent-failed-operations"></a>4: chybové zprávy pro poslední neúspěšné operace zaznamenány do protokolu

`$SeparateDscOperations[0].Group` obsahuje sadu událostí pro poslední operaci. Spustit `Where-Object` rutiny filtrovat události podle jejich úrovně zobrazovaný název. Výsledky jsou uloženy ve `$myFailedEvent` proměnné, které může být dále odebrán k získání zprávy událostí:

```powershell
PS C:\> $myFailedEvent = ($SeparateDscOperations[0].Group | Where-Object {$_.LevelDisplayName -eq "Error"})
 
PS C:\> $myFailedEvent.Message
Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} : 
DSC Engine Error : 
 Error Message Current configuration does not exist. Execute Start-DscConfiguration command with -Path pa
rameter to specify a configuration file and create a current configuration first. 
Error Code : 1 
```

### <a name="5-all-events-generated-for-a-particular-job-id"></a>5: všechny události vytvořené pro konkrétní úlohy ID.

`$SeparateDscOperations` je pole skupiny, z nichž každá má název jako úlohy jedinečné ID. Spuštěním `Where-Object` rutiny, můžete rozbalit těchto skupin události, které mají ID konkrétní úlohy:

```powershell
PS C:\> ($SeparateDscOperations | Where-Object {$_.Name -eq $jobX} ).Group

   ProviderName: Microsoft-Windows-DSC
 
TimeCreated                     Id LevelDisplayName Message                                               
-----------                     -- ---------------- -------                                               
12/2/2013 4:33:24 PM          4102 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...      
12/2/2013 4:33:24 PM          4168 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...      
12/2/2013 4:33:24 PM          4146 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...      
12/2/2013 4:33:24 PM          4120 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...  
```

## <a name="using-xdscdiagnostics-to-analyze-dsc-logs"></a>Použití xDscDiagnostics k analýze DSC protokolů

**xDscDiagnostics** je modul prostředí PowerShell, který se skládá z několika funkce, které může pomoci analýza selhání DSC v počítači. Tyto funkce můžete identifikovat všechny místní události z posledních DSC operace nebo DSC událostí na vzdálených počítačích (s platné přihlašovací údaje). Zde termín DSC operace se používá k definování jednoho jedinečný spuštění DSC od jeho začátku jeho koncem. Například `Test-DscConfiguration` by samostatné operace DSC. Podobně každé další rutině v DSC (například `Get-DscConfiguration`, `Start-DscConfiguration`atd) může každý musí identifikovat jako samostatné operace DSC. Funkce jsou vysvětlené v [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics). Je k dispozici nápověda spuštěním `Get-Help <cmdlet name>`.

### <a name="getting-details-of-dsc-operations"></a>Získávání podrobností DSC operací 

`Get-xDscOperation` Funkce umožňuje najít výsledky operací DSC, které běží na jeden nebo více počítačů a vrátí objekt, který obsahuje kolekci událostí produkovaný každou operaci DSC. V následující výstup, například tři příkazy byly spuštěné. První z nich předán a dalších dvou selhalo. Tyto výsledky jsou shrnuty v rámci výstupu `Get-xDscOperation`.

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation

ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents            
------------   ---------- -----------           ------   -----                                 ---------            
SRV1   1          6/23/2016 9:37:52 AM  Failure  9701aadf-395e-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   2          6/23/2016 9:36:54 AM  Failure  7e8e2d6e-395c-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   3          6/23/2016 9:36:54 AM  Success  af72c6aa-3960-11e6-9165-00155d390509  {@{Message=Operati...

```

Můžete také určit, mají jenom výsledky pro poslední operace pomocí `Newest` parametr:

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation -Newest 5
ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents            
------------   ---------- -----------           ------   -----                                 ---------            
SRV1   1          6/23/2016 4:36:54 PM  Success                                        {@{Message=; TimeC...
SRV1   2          6/23/2016 4:36:54 PM  Success  5c06402b-399b-11e6-9165-00155d390509  {@{Message=Operati...
SRV1   3          6/23/2016 4:36:54 PM  Success                                        {@{Message=; TimeC...
SRV1   4          6/23/2016 4:36:54 PM  Success  5c06402a-399b-11e6-9165-00155d390509  {@{Message=Operati...
SRV1   5          6/23/2016 4:36:51 PM  Success                                        {@{Message=; TimeC...
```

### <a name="getting-details-of-dsc-events"></a>Získávání podrobností DSC událostí

`Trace-xDscOperation` Rutina vrátí objekt, který obsahuje kolekci událostí, jejich typy událostí, a zpráva výstupní generované z konkrétní operace DSC. Obvykle, když najít selhání v žádném z operace pomocí `Get-xDscOperation`, by trasování činnosti s cílem zjistit, které události způsobila selhání.

Použití `SequenceID` k načtení události pro konkrétní operaci pro určitý počítač. Pokud zadáte například `SequenceID` 9, `Trace-xDscOperaion` získat trasování pro operace DSC, která byla 9. z poslední operace:

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -SequenceID 9

ComputerName   EventType    TimeCreated           Message                                                                                             
------------   ---------    -----------           -------                                                                                             
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM Operation Consistency Check or Pull started by user sid S-1-5-20 from computer NULL.                
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM Running consistency engine.                                                                         
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM The local configuration manager is updating the PSModulePath to WindowsPowerShell\Modules;C:\Prog...
SRV1   OPERATIONAL  6/24/2016 10:51:53 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature, [xDSCWebService]PSDSCPullServer. 
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Consistency engine was run successfully.                                                            
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Job runs under the following LCM setting. ...                                                       
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Operation Consistency Check or Pull completed successfully. 
```

Předat **GUID** přiřazený konkrétní operaci DSC (jak ho vrátila `Get-xDscOperation` cmldet) získat podrobnosti o události pro tuto operaci DSC:

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -JobID 9e0bfb6b-3a3a-11e6-9165-00155d390509

ComputerName   EventType    TimeCreated           Message                                                                                             
------------   ---------    -----------           -------                                                                                             
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull started by user sid S-1-5-20 from computer NULL.                
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof                             
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Running consistency engine.                                                                         
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [] Starting consistency engine.                          
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Applying configuration from C:\Windows\System32\Configuration\Current.mof.                          
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Parsing the configuration to apply.                                                                 
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature, [xDSCWebService]PSDSCPullServer. 
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Resource ]  [[WindowsFeature]DSCServiceFeature]                      
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_RoleResource with resource name [WindowsFeature]DSC...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Test     ]  [[WindowsFeature]DSCServiceFeature]                      
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[WindowsFeature]DSCServiceFeature] The operation 'Get...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[WindowsFeature]DSCServiceFeature] The operation 'Get...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Test     ]  [[WindowsFeature]DSCServiceFeature] True in 0.3130 sec...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Resource ]  [[WindowsFeature]DSCServiceFeature]                      
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Resource ]  [[xDSCWebService]PSDSCPullServer]                        
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_xDSCWebService with resource name [xDSCWebService]P...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Test     ]  [[xDSCWebService]PSDSCPullServer]                        
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Ensure           
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Port             
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Physical Path ...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check State            
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Get Full Path for We...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Test     ]  [[xDSCWebService]PSDSCPullServer] True in 0.0160 seconds.
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Resource ]  [[xDSCWebService]PSDSCPullServer]                        
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [] Consistency check completed.                          
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof                             
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Consistency engine was run successfully.                                                            
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Job runs under the following LCM setting. ...                                                       
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull completed successfully.                                         
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof
```

Všimněte si, že, protože `Trace-xDscOperation` agreguje události z analýzu, ladění a provozní protokoly, vás vyzve k povolení těchto protokolů, jak je popsáno výše.

Alternativně můžete shromáždit informace o události uložením výstup `Trace-xDscOperation` do proměnné. Pokud chcete zobrazit všechny události pro konkrétní operaci DSC můžete následující příkazy.

```powershell
PS C:\DiagnosticsTest> $Trace = Trace-xDscOperation -SequenceID 4

PS C:\DiagnosticsTest> $Trace.Event
```

Zobrazí se stejné výsledky jako `Get-WinEvent` rutiny, například následující výstup:

```powershell
   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message                                                                                           
-----------                     -- ---------------- -------                                                                                           
6/23/2016 1:36:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 1:36:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 2:07:00 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 2:07:01 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 2:36:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 2:36:56 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 3:06:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 3:06:55 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 3:36:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 3:36:55 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 4:06:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 4:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 4:36:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 4:36:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 5:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 5:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 5:36:54 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 5:36:54 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 6:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 6:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 6:36:56 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 6:36:57 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 7:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 7:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 7:36:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 7:36:54 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 8:06:54 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
```

V ideálním případě byste nejdřív použili `Get-xDscOperation` seznam se posledních několik DSC konfigurace běží na vašich počítačích. Při tomto postupu můžete zkontrolovat všechny najednou (pomocí jeho SequenceID nebo JobID) s `Trace-xDscOperation` chcete zjistit, co se na pozadí.

### <a name="getting-events-for-a-remote-computer"></a>Získávání události ve vzdáleném počítači

Použití `ComputerName` parametr `Trace-xDscOperation` rutiny získat podrobnosti o události ve vzdáleném počítači. Předtím, než můžete provést, je nutné vytvořit pravidlo brány firewall pro povolení vzdálené správy na vzdáleném počítači:

```powershell
New-NetFirewallRule -Name "Service RemoteAdmin" -DisplayName "Remote" -Action Allow
```
Teď zadáte tento počítač v volání `Trace-xDscOperation`:

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -ComputerName SRV2 -Credential Get-Credential -SequenceID 5

ComputerName   EventType    TimeCreated           Message
------------   ---------    -----------           -------
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull started by user sid S-1-5-20 f...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Running consistency engine.
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [] Starting consistency...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Applying configuration from C:\Windows\System32\Configuration\Curr...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Parsing the configuration to apply.
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature,...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Resource ]  [[WindowsFeature]DSCSer...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_RoleResource with re...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Test     ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Test     ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Resource ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Resource ]  [[xDSCWebService]PSDSCP...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_xDSCWebService with ...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Test     ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Test     ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Resource ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [] Consistency check co...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Consistency engine was run successfully.
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Job runs under the following LCM setting. ...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull completed successfully.
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
```

## <a name="my-resources-wont-update-how-to-reset-the-cache"></a>Moje prostředky nebude aktualizovat: obnovení mezipaměti

Modul DSC ukládá do mezipaměti prostředky, které jsou implementované jako modul prostředí PowerShell pro účely efektivitu. To však může způsobit problémy, při vytváření prostředku a současně ho testování, protože DSC načte verze v mezipaměti, dokud proces nebude znovu spuštěna. Jediný způsob, jak provést DSC načíst novější verze je explicitně ukončit proces DSC modul hostování.

Podobně když spustíte `Start-DscConfiguration`, po přidání a úpravy vlastní prostředek, nemusí provést úpravy, pokud nebo do doby, po restartování počítače. Je to proto DSC běží v procesu hostitele zprostředkovatele rozhraní WMI (WmiPrvSE) a obvykle existuje velký počet instancí WmiPrvSE systémem najednou. Když restartujete, musí hostitelský proces restartování a nevymažete mezipaměť.

K úspěšnému recyklovat konfigurace a vymažte mezipaměť bez nutnosti restartování, musíte zastavit a znovu spusťte proces hostitele. Tento krok můžete provést na základě za instance, kterým identifikovat proces, případně ji zastavte a restartujte ji. Nebo můžete použít `DebugMode`, jak je znázorněno níže, znovu načíst prostředek DSC prostředí PowerShell.

K identifikaci procesu, který je hostitelem modul DSC a zastavte ji na základě za instance, můžete vytvořit seznam ID procesu WmiPrvSE, který je hostitelem modul DSC. Poté, chcete-li aktualizovat zprostředkovatele, zastavit proces WmiPrvSE pomocí níže uvedených příkazů a potom spusťte **Start-DscConfiguration** znovu.

```powershell
###
### find the process that is hosting the DSC engine
###
$dscProcessID = Get-WmiObject msft_providers | 
Where-Object {$_.provider -like 'dsccore'} | 
Select-Object -ExpandProperty HostProcessIdentifier 

###
### Stop the process
###
Get-Process -Id $dscProcessID | Stop-Process
```

## <a name="using-debugmode"></a>Pomocí režim DebugMode

Můžete nakonfigurovat DSC místní Configuration Manager (LCM) používat `DebugMode` vždy vymazání mezipaměti při restartování procesu hostitele. Pokud nastavíte hodnotu **TRUE**, způsobí, že modul vždy načtením prostředek DSC prostředí PowerShell. Po dokončení zápisu prostředek, můžete ho nastavit zpět na **FALSE** a modul bude používat své chování ukládání do mezipaměti, moduly.

Následuje ukázka zobrazíte jak `DebugMode` můžete automaticky aktualizace mezipaměti. První Podíváme se na výchozí konfigurace:

```
PS C:\> Get-DscLocalConfigurationManager
 
 
AllowModuleOverwrite           : False
CertificateID                  : 
ConfigurationID                : 
ConfigurationMode              : ApplyAndMonitor
ConfigurationModeFrequencyMins : 30
Credential                     : 
DebugMode                      : False
DownloadManagerCustomData      : 
DownloadManagerName            : 
LocalConfigurationManagerState : Ready
RebootNodeIfNeeded             : False
RefreshFrequencyMins           : 15
RefreshMode                    : PUSH
PSComputerName                 :  
```

Uvidíte, že `DebugMode` je nastaven na **FALSE**.

Nastavit `DebugMode` ukázku, použijte následující zdroj prostředí PowerShell:

```powershell
function Get-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    return @{onlyProperty = Get-Content -Path "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"}
}
function Set-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    "1" | Out-File -PSPath "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"
}
function Test-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    return $false
} 
```

Nyní vytváření konfigurace pomocí výše prostředek s názvem `TestProviderDebugMode`:

```powershell
Configuration ConfigTestDebugMode
{
    Import-DscResource -Name TestProviderDebugMode
    Node localhost
    {
        TestProviderDebugMode test
        {
            onlyProperty = "blah"
        }
    }
}
ConfigTestDebugMode
```

Zobrazí se obsah souboru: "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**" je **1**.

Nyní aktualizujte zprostředkovatele kódu, pomocí následujícího skriptu:

```powershell
$newResourceOutput = Get-Random -Minimum 5 -Maximum 30
$content = @"
function Get-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    return @{onlyProperty = Get-Content -Path "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"}
}
function Set-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    "$newResourceOutput" | Out-File -PSPath C:\OutputFromTestProviderDebugMode.txt
}
function Test-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    return `$false
}
"@ | Out-File -FilePath "C:\Program Files\WindowsPowerShell\Modules\MyPowerShellModules\DSCResources\TestProviderDebugMode\TestProviderDebugMode.psm1
```

Tento skript generuje náhodné číslo a příslušným způsobem aktualizuje kód zprostředkovatele. S `DebugMode` nastavena na hodnotu false, obsah souboru "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**" nikdy došlo ke změně.

Nyní nastavte `DebugMode` k **TRUE** v konfigurační skript:

```powershell
LocalConfigurationManager
{
    DebugMode = $true
} 
```

Když znovu spustíte skript výše, zobrazí se, že obsah souboru je jiný pokaždé, když. (Můžete spustit `Get-DscConfiguration` zaškrtněte je). Níže je výsledkem dva další běží (výsledky mohou lišit při spuštění skriptu):

```powershell
PS C:\> Get-DscConfiguration -CimSession (New-CimSession localhost)
 
onlyProperty                            PSComputerName                         
------------                            --------------                         
20                                      localhost                              
 
PS C:\> Get-DscConfiguration -CimSession (New-CimSession localhost)
 
onlyProperty                            PSComputerName                         
------------                            --------------                         
14                                      localhost
```

## <a name="see-also"></a>Viz také

### <a name="reference"></a>Referenční informace
* [Prostředek DSC protokolu](logResource.md)

### <a name="concepts"></a>Koncepty
* [Sestavení vlastní Windows PowerShell Desired State Configuration prostředky](authoringResource.md)

### <a name="other-resources"></a>Další prostředky
* [Požadovaného stavu konfiguračních rutin prostředí Windows PowerShell](https://technet.microsoft.com/library/dn521624(v=wps.630).aspx)

