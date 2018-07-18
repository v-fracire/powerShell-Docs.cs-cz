---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Řešení potíží s DSC
ms.openlocfilehash: 1e8bfdf3540e65e3be94bf6a9b04e7d3b14ff044
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39094064"
---
# <a name="troubleshooting-dsc"></a>Řešení potíží s DSC

>Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Toto téma popisuje způsoby řešení potíží s DSC při vzniknou problémy.

## <a name="winrm-dependency"></a>Služba WinRM závislostí

Windows PowerShell Desired State Configuration (DSC) závisí na WinRM. Ve výchozím nastavení v systému Windows Server 2008 R2 a Windows 7 není povolená služba WinRM. Spustit ```Set-WSManQuickConfig```, ve Windows Powershellu se zvýšenými oprávněními relace, aby Služba WinRM.

## <a name="using-get-dscconfigurationstatus"></a>Pomocí Get-DscConfigurationStatus

[Get-DscConfigurationStatus](https://technet.microsoft.com/library/mt517868.aspx) rutina načte informace o konfiguraci stavu z cílového uzlu.
Bohaté objekt je vrácen, který zahrnuje souhrnné informace o Určuje, jestli spuštění konfigurace byla nebo nebyla úspěšná. Při prozkoumávání objekt, který chcete zjistit podrobnosti o konfiguraci, jako je:

- Všechny prostředky, které selhaly
- Prostředek, který požaduje restartování
- Meta-konfigurace nastavení v době konfigurace spuštění
- Atd.

Následující sada parametrů vrátí informace o stavu pro poslední konfigurace spuštění:

```powershell
Get-DscConfigurationStatus  [-CimSession <CimSession[]>]
                            [-ThrottleLimit <int>]
                            [-AsJob]
                            [<CommonParameters>]
```
Následující sada parametrů vrátí informace o stavu pro všechny předchozí konfigurace spuštění:

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

## <a name="my-script-wont-run-using-dsc-logs-to-diagnose-script-errors"></a>Tento skript se nespustí: pomocí DSC protokoly pro diagnostiku chyby skriptu

Stejně jako všechny software Windows DSC zaznamenává chyby a události v [protokoly](https://msdn.microsoft.com/library/windows/desktop/aa363632.aspx) , který si můžete prohlížet [Prohlížeč událostí](http://windows.microsoft.com/windows/what-information-event-logs-event-viewer). Zkoumání tyto protokoly pomůžou pochopit, proč určité operace se nezdařila a jak zabránit selhání v budoucnu. Psaní konfiguračních skriptů může být velmi obtížné, proto kvůli jako autor můžete zjednodušit sledování chyb, použít prostředek DSC Log ke sledování pokroku vaší konfigurace DSC analytického protokolu událostí.

## <a name="where-are-dsc-event-logs"></a>Kde jsou protokoly událostí DSC?

V prohlížeči událostí, jsou události DSC v: **aplikací a služeb protokoly/Microsoft/Windows/Desired State Configuration**

Odpovídající rutiny prostředí PowerShell [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx), můžete spustit také zobrazit protokoly událostí:

```
PS C:\> Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
   ProviderName: Microsoft-Windows-DSC
TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
11/17/2014 10:27:23 PM        4102 Information      Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} :
```

Jak uvádíme výš, je název vaší DSC primární protokolu **Microsoft -> Windows -> DSC** (jiné názvy protokolů v rámci Windows nejsou zobrazené pro zkrácení). Primární název je připojeným k názvu kanálu k vytvoření názvu úplný protokol. Modul DSC zapíše hlavně na tři typy protokolů: [provozní, analýzu a ladit protokoly](https://technet.microsoft.com/library/cc722404.aspx). Od analýzy a protokoly ladění jsou ve výchozím nastavení vypnuta, měli byste povolit v prohlížeči událostí. Chcete-li to provést, otevřete Prohlížeč událostí tak, že zadáte zobrazit protokolu událostí Windows PowerShell nebo klikněte na tlačítko **Start** tlačítko, klikněte na tlačítko **ovládací panely**, klikněte na tlačítko **nástroje pro správu**a potom klikněte na tlačítko **Prohlížeč událostí**. Na **zobrazení** klikněte na tlačítko nabídky v prohlížeči událostí **zobrazit protokoly ladění a analýzu**. Název protokolu analytického kanálu je **Microsoft-Windows-Dsc/analytické**, a je kanál ladění **Microsoft-Windows-Dsc/Debug**. Můžete také použít [wevtutil](https://technet.microsoft.com/library/cc732848.aspx) nástroj a povolte je, jak je znázorněno v následujícím příkladu.

```powershell
wevtutil.exe set-log “Microsoft-Windows-Dsc/Analytic” /q:true /e:true
```

## <a name="what-do-dsc-logs-contain"></a>Co neobsahují DSC protokoly?

Protokoly DSC se rozdělit přes tři kanály protokolu na základě důležitosti zprávy. Operační protokol v DSC obsahuje všechny chybové zprávy a je možné identifikovat problém. Analytický protokol má větší objem událostí a zjistit, kde došlo k chybě. Tento kanál obsahuje také podrobné zprávy (pokud existuje). Protokol ladění obsahuje protokoly, které vám pomůžou pochopit, jak došlo k chybám. Zprávy o událostech DSC strukturovány tak, aby všechny zprávy událostí začne s ID úlohy, který jedinečně reprezentuje operaci DSC. Následující příklad se pokusí získat zprávu od první událost, která je zaznamenána do protokolu provozní DSC.

```powershell
PS C:\> $AllDscOpEvents = Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
PS C:\> $FirstOperationalEvent = $AllDscOpEvents[0]
PS C:\> $FirstOperationalEvent.Message
Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} :
Consistency engine was run successfully.
```

DSC události jsou protokolovány v konkrétní strukturu, která umožňuje uživateli pro agregaci událostí z jednoho projektu DSC. Struktura je následujícím způsobem:

**ID úlohy: \<Guid\>**
**\<zpráva o události\>**

## <a name="gathering-events-from-a-single-dsc-operation"></a>Shromažďování událostí v rámci jedné operace DSC

Protokoly událostí DSC obsahovat události generované modulem různé operace DSC. Ale obvykle budete s detaily zajímá jenom jeden konkrétní operace. Všechny protokoly DSC můžete seskupit podle vlastnosti ID úlohy, které jsou jedinečné pro každé operace DSC. ID úlohy se zobrazí jako první hodnota vlastnosti ve všech událostí DSC. Následující postup vysvětluje, jak k shromažďování všech událostí ve struktuře seskupených pole.

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

Tady, proměnná `$SeparateDscOperations` obsahuje protokoly, které jsou seskupeny podle ID úloh. Každý prvek pole této proměnné představuje skupinu události zapsané podle jiné operace DSC, povolení přístupu na další informace o protokolech.

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

Můžete extrahovat data v proměnné `$SeparateDscOperations` pomocí [Where-Object](https://technet.microsoft.com/library/ee177028.aspx). Níže jsou pět scénáře, ve kterých můžete extrahovat data pro řešení potíží s DSC:

### <a name="1-operations-failures"></a>1: selhání operací

Všechny události mají [úrovně závažnosti](https://msdn.microsoft.com/library/dd996917(v=vs.85)). Tyto informace slouží k identifikaci chybové události:

```
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.LevelDisplayName -contains "Error"}
Count Name                      Group
----- ----                      -----
   38 {5BCA8BE7-5BB6-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
```

### <a name="2-details-of-operations-run-in-the-last-half-hour"></a>2: spuštění podrobnosti operace v poslední půlhodiny

`TimeCreated`, vlastnost všech událostí Windows uvádí čas vytvoření události. Porovnání s objektem konkrétní datum a čas tato vlastnost slouží k filtrování všechny události:

```powershell
PS C:\> $DateLatest = (Get-Date).AddMinutes(-30)
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.TimeCreated -gt $DateLatest}
Count Name                      Group
----- ----                      -----
    1 {6CEC5B09-5BB0-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord}
```

### <a name="3-messages-from-the-latest-operation"></a>3: zprávy z nejnovější operace

Nejnovější operace je uložen v první index pole skupiny `$SeparateDscOperations`. Dotazování skupiny zpráv pro index 0, vrátí se všechny zprávy o poslední operaci:

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

### <a name="4-error-messages-logged-for-recent-failed-operations"></a>4: chybové zprávy pro poslední neúspěšné operace

`$SeparateDscOperations[0].Group` obsahuje sadu událostí pro poslední operaci. Spustit `Where-Object` rutiny filtrovat události podle jejich úrovně zobrazovaného jména. Výsledky jsou uloženy v `$myFailedEvent` proměnné, která může být dále odebrán zobrazíte zpráva o události:

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

`$SeparateDscOperations` je pole skupin, z nichž každá má název jako úlohy jedinečné ID. Spuštěním `Where-Object` rutiny, můžete extrahovat těchto skupin události, které mají ID konkrétní úlohy:

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

## <a name="using-xdscdiagnostics-to-analyze-dsc-logs"></a>Použití xDscDiagnostics k analýze DSC protokoly

**xDscDiagnostics** je modul Powershellu, které obsahuje několik funkcí, které vám mohou pomoci analýza selhání DSC na svém počítači. Tyto funkce můžete identifikovat všechny místní akce z poslední DSC operace nebo události DSC na vzdálených počítačích (se platné přihlašovací údaje). Termín DSC operace tady, se používá k definování jeden jedinečný spuštění DSC od jeho začátku jeho ukončení. Například `Test-DscConfiguration` by samostatné operaci DSC. Podobně, každý další rutiny v DSC (například `Get-DscConfiguration`, `Start-DscConfiguration`atd) každý nelze identifikovat jako samostatné operace DSC. Funkce jsou vysvětleny v [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics).
Není k dispozici nápověda spuštěním `Get-Help <cmdlet name>`.

### <a name="getting-details-of-dsc-operations"></a>Získávání podrobností operací DSC

`Get-xDscOperation` Funkce vám umožní najít výsledky operací DSC, které běží na jeden nebo více počítačů a vrátí objekt, který obsahuje kolekci událostí produkovaný každou operaci DSC.
V následující výstup například tři příkazy byly spuštěny. Předaný první a druhé dvě selhala. Tyto výsledky jsou shrnuty v rámci výstupu `Get-xDscOperation`.

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation

ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents
------------   ---------- -----------           ------   -----                                 ---------
SRV1   1          6/23/2016 9:37:52 AM  Failure  9701aadf-395e-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   2          6/23/2016 9:36:54 AM  Failure  7e8e2d6e-395c-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   3          6/23/2016 9:36:54 AM  Success  af72c6aa-3960-11e6-9165-00155d390509  {@{Message=Operati...
```

Můžete také určit, který má pouze výsledky pro poslední operace s použitím `Newest` parametr:

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

### <a name="getting-details-of-dsc-events"></a>Získávání podrobností o události DSC

`Trace-xDscOperation` Rutina vrátí objekt, který obsahuje kolekci událostí, jejich typy událostí, a výstupní zprávy generované určitou operaci DSC. Obvykle, když najdete selhání v některém z operací pomocí `Get-xDscOperation`, by trasování činnosti s cílem zjistit, která z události způsobila chybu.

Použití `SequenceID` parametr získat události pro konkrétní operaci pro určitý počítač. Pokud zadáte například `SequenceID` 9, `Trace-xDscOperaion` získat trasování pro operace DSC, která byla 9 od poslední operace:

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

Předání **GUID** přiřazené k určité operace DSC (vrácené `Get-xDscOperation` cmldet) zobrazíte podrobnosti o události pro tuto operaci DSC:

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

Všimněte si, že od té doby `Trace-xDscOperation` agreguje události z analýzy, ladění a provozní protokoly, vás vyzve k povolení těchto protokolů, jak je popsáno výše.

Alternativně můžete shromáždit informace o událostech prostřednictvím ukládání výstupu `Trace-xDscOperation` do proměnné. Pokud chcete zobrazit všechny události pro určitou operaci DSC můžete použít následující příkazy.

```powershell
PS C:\DiagnosticsTest> $Trace = Trace-xDscOperation -SequenceID 4

PS C:\DiagnosticsTest> $Trace.Event
```

Zobrazí se stejné výsledky jako `Get-WinEvent` rutiny, jako je například následující výstup:

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

V ideálním případě byste nejdřív použili `Get-xDscOperation` na seznam posledních několika DSC konfigurace běží na vašich počítačích. Při tomto postupu můžete prozkoumat všechny najednou (pomocí jeho SequenceID nebo JobID) s `Trace-xDscOperation` zjistit, co jste na pozadí.

### <a name="getting-events-for-a-remote-computer"></a>Získat události na vzdálený počítač

Použití `ComputerName` parametr `Trace-xDscOperation` rutiny pro získání podrobností událostí na vzdáleném počítači. Předtím, než můžete provést, je nutné vytvořit pravidlo brány firewall pro povolení vzdálené správy na vzdáleném počítači:

```powershell
New-NetFirewallRule -Name "Service RemoteAdmin" -DisplayName "Remote" -Action Allow
```
Nyní zadáte tento počítač při volání funkce vaše `Trace-xDscOperation`:

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

## <a name="my-resources-wont-update-how-to-reset-the-cache"></a>Moje prostředky se neaktualizuje: Resetování mezipaměti

Modul DSC prostředky, které jsou implementovány jako modul Powershellu pro účely efektivitu ukládá do mezipaměti. Nicméně to může způsobit problémy při vytváření prostředku a otestujete ji současně, protože DSC načte verze uložené v mezipaměti až po restartování procesu. Jediný způsob, jak provést DSC načíst novější verze je explicitně ukončení procesu, který je hostitelem modulu DSC.

Podobně, když spustíte `Start-DscConfiguration`, po přidání a úpravy vlastní prostředek, pravděpodobně nebude spuštěna úpravy, není-li nebo, dokud nebude počítač restartován. Je to proto DSC běží v hostitelském procesu zprostředkovatele rozhraní WMI (WmiPrvSE) a existují obvykle velký počet instancí WmiPrvSE najednou spuštěna. Když restartujete, restartování hostitelského procesu a nevymažete mezipaměť.

Úspěšně recyklovat konfiguraci a vymažte její mezipaměť bez nutnosti restartování, musíte zastavit a poté restartujte hostitelský proces. To můžete udělat na na základě instancí, kterým Identifikujte proces, zastavte ji a restartujte ji. Nebo můžete použít `DebugMode`, jak je znázorněno níže, k opětovnému načtení prostředků DSC Powershellu.

K identifikaci, který proces je hostitelem modulu DSC a zastavte ji na na základě instancí, můžete vytvořit seznam ID procesu sady WmiPrvSE, který je hostitelem modulu DSC. Poté, aktualizovat poskytovatele, zastavte WmiPrvSE procesu pomocí níže uvedených příkazů a potom spusťte **Start-DscConfiguration** znovu.

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

## <a name="using-debugmode"></a>Režim DebugMode pomocí

Můžete nakonfigurovat DSC místní Configuration Manageru (LCM) používat `DebugMode` a vždy vymažte mezipaměť při restartování hostitelského procesu. Pokud je nastavena na **TRUE**, způsobí, že modul, aby vždy znovu načíst prostředek DSC Powershellu. Po dokončení zápisu váš prostředek, můžete ho nastavit zpět **FALSE** a modul bude používat pro své chování ukládání do mezipaměti moduly.

Tady je ukázka zobrazíte jak `DebugMode` můžete automaticky aktualizovat mezipaměť. Nejprve Podívejme se na výchozí konfigurace:

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

Vidíte, že `DebugMode` je nastavena na **FALSE**.

Nastavit `DebugMode` ukázku, použijte následující prostředek prostředí PowerShell:

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

Nyní, vytváření konfigurace pomocí výše uvedených prostředků volá `TestProviderDebugMode`:

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

Uvidíte, že obsah souboru: "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**" je **1**.

Nyní aktualizace zprostředkovatele kódu pomocí následujícího skriptu:

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

Tento skript generuje náhodné číslo a odpovídajícím způsobem aktualizuje zprostředkovatele kódu. S `DebugMode` nastavena na hodnotu false, obsah souboru "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**" se nikdy změněn.

Nyní nastavte `DebugMode` k **TRUE** v konfigurační skript:

```powershell
LocalConfigurationManager
{
    DebugMode = $true
}
```

Když znovu spustíte výše uvedené skript, uvidíte, že obsah souboru se liší pokaždé, když. (Můžete spustit `Get-DscConfiguration` tak zkontrolovat, že). Níže je výsledek dvě další spuštění (výsledky mohou lišit při spuštění skriptu):

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

- [Prostředek DSC Log](logResource.md)

### <a name="concepts"></a>Koncepty

- [Vlastní Windows PowerShell Desired State Configuration prostředky sestavení](authoringResource.md)

### <a name="other-resources"></a>Další prostředky

- [Prostředí Windows PowerShell Desired State Configuration rutiny](https://technet.microsoft.com/library/dn521624(v=wps.630).aspx)