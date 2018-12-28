---
ms.date: 10/30/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Řešení potíží s DSC
ms.openlocfilehash: e1f36bbc97569ac0d65f003ee08f52ec174a4520
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403816"
---
# <a name="troubleshooting-dsc"></a><span data-ttu-id="77164-103">Řešení potíží s DSC</span><span class="sxs-lookup"><span data-stu-id="77164-103">Troubleshooting DSC</span></span>

<span data-ttu-id="77164-104">_Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0_</span><span class="sxs-lookup"><span data-stu-id="77164-104">_Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0_</span></span>

<span data-ttu-id="77164-105">Toto téma popisuje způsoby řešení potíží s DSC při vzniknou problémy.</span><span class="sxs-lookup"><span data-stu-id="77164-105">This topic describes ways to troubleshoot DSC when problems arise.</span></span>

## <a name="winrm-dependency"></a><span data-ttu-id="77164-106">Služba WinRM závislostí</span><span class="sxs-lookup"><span data-stu-id="77164-106">WinRM Dependency</span></span>

<span data-ttu-id="77164-107">Windows PowerShell Desired State Configuration (DSC) závisí na WinRM.</span><span class="sxs-lookup"><span data-stu-id="77164-107">Windows PowerShell Desired State Configuration (DSC) depends on WinRM.</span></span> <span data-ttu-id="77164-108">Ve výchozím nastavení v systému Windows Server 2008 R2 a Windows 7 není povolená služba WinRM.</span><span class="sxs-lookup"><span data-stu-id="77164-108">WinRM is not enabled by default on Windows Server 2008 R2 and Windows 7.</span></span> <span data-ttu-id="77164-109">Spustit `Set-WSManQuickConfig`, ve Windows Powershellu se zvýšenými oprávněními relace, aby Služba WinRM.</span><span class="sxs-lookup"><span data-stu-id="77164-109">Run `Set-WSManQuickConfig`, in a Windows PowerShell elevated session, to enable WinRM.</span></span>

## <a name="using-get-dscconfigurationstatus"></a><span data-ttu-id="77164-110">Pomocí Get-DscConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="77164-110">Using Get-DscConfigurationStatus</span></span>

<span data-ttu-id="77164-111">[Get-DscConfigurationStatus](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus) rutina načte informace o konfiguraci stavu z cílového uzlu.</span><span class="sxs-lookup"><span data-stu-id="77164-111">The [Get-DscConfigurationStatus](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus) cmdlet gets information about configuration status from a target node.</span></span> <span data-ttu-id="77164-112">Bohaté objekt je vrácen, který zahrnuje souhrnné informace o Určuje, jestli spuštění konfigurace byla nebo nebyla úspěšná.</span><span class="sxs-lookup"><span data-stu-id="77164-112">A rich object is returned that includes high-level information about whether or not the configuration run was successful or not.</span></span> <span data-ttu-id="77164-113">Při prozkoumávání objekt, který chcete zjistit podrobnosti o konfiguraci, jako je:</span><span class="sxs-lookup"><span data-stu-id="77164-113">You can dig into the object to discover details about the configuration run such as:</span></span>

- <span data-ttu-id="77164-114">Všechny prostředky, které selhaly</span><span class="sxs-lookup"><span data-stu-id="77164-114">All of the resources that failed</span></span>
- <span data-ttu-id="77164-115">Prostředek, který požaduje restartování</span><span class="sxs-lookup"><span data-stu-id="77164-115">Any resource that requested a reboot</span></span>
- <span data-ttu-id="77164-116">Meta-konfigurace nastavení v době konfigurace spuštění</span><span class="sxs-lookup"><span data-stu-id="77164-116">Meta-Configuration settings at time of configuration run</span></span>
- <span data-ttu-id="77164-117">Atd.</span><span class="sxs-lookup"><span data-stu-id="77164-117">Etc.</span></span>

<span data-ttu-id="77164-118">Následující sada parametrů vrátí informace o stavu pro poslední konfigurace spuštění:</span><span class="sxs-lookup"><span data-stu-id="77164-118">The following parameter set returns the status information for the last configuration run:</span></span>

```
Get-DscConfigurationStatus [-CimSession <CimSession[]>]
                           [-ThrottleLimit <int>]
                           [-AsJob]
                           [<CommonParameters>]
```
<span data-ttu-id="77164-119">Následující sada parametrů vrátí informace o stavu pro všechny předchozí konfigurace spuštění:</span><span class="sxs-lookup"><span data-stu-id="77164-119">The following parameter set returns the status information for all previous configuration runs:</span></span>

```
Get-DscConfigurationStatus -All
                           [-CimSession <CimSession[]>]
                           [-ThrottleLimit <int>]
                           [-AsJob]
                           [<CommonParameters>]
```

## <a name="example"></a><span data-ttu-id="77164-120">Příklad</span><span class="sxs-lookup"><span data-stu-id="77164-120">Example</span></span>

```powershell
PS C:\> $Status = Get-DscConfigurationStatus

PS C:\> $Status

Status         StartDate                Type            Mode    RebootRequested        NumberOfResources
------        ---------                ----            ----    ---------------        -----------------
Failure        11/24/2015  3:44:56     Consistency        Push    True                36

PS C:\> $Status.ResourcesNotInDesiredState

ConfigurationName     :    MyService
DependsOn             :
ModuleName            :    PSDesiredStateConfiguration
ModuleVersion         :    1.1
PsDscRunAsCredential  :
ResourceID            :    [File]ServiceDll
SourceInfo            :    c:\git\CustomerService\Configs\MyCustomService.ps1::5::34::File
DurationInSeconds     :    0.19
Error                 :    SourcePath must be accessible for current configuration. The related file/directory is:
                           \\Server93\Shared\contosoApp.dll. The related ResourceID is [File]ServiceDll
FinalState            :
InDesiredState        :    False
InitialState          :
InstanceName          :    ServiceDll
RebootRequested       :    False
ReosurceName          :    File
StartDate             :    11/24/2015  3:44:56
PSComputerName        :
```

## <a name="my-script-wont-run-using-dsc-logs-to-diagnose-script-errors"></a><span data-ttu-id="77164-121">Tento skript se nespustí: Použití DSC protokoly pro diagnostiku chyby skriptu</span><span class="sxs-lookup"><span data-stu-id="77164-121">My script won't run: Using DSC logs to diagnose script errors</span></span>

<span data-ttu-id="77164-122">Stejně jako všechny software Windows DSC zaznamenává chyby a události v [protokoly](/windows/desktop/EventLog/about-event-logging) , který si můžete prohlížet [Prohlížeč událostí](https://support.microsoft.com/hub/4338813/windows-help).</span><span class="sxs-lookup"><span data-stu-id="77164-122">Like all Windows software, DSC records errors and events in [logs](/windows/desktop/EventLog/about-event-logging) that can be viewed from the [Event Viewer](https://support.microsoft.com/hub/4338813/windows-help).</span></span>
<span data-ttu-id="77164-123">Zkoumání tyto protokoly pomůžou pochopit, proč určité operace se nezdařila a jak zabránit selhání v budoucnu.</span><span class="sxs-lookup"><span data-stu-id="77164-123">Examining these logs can help you understand why a particular operation failed, and how to prevent failure in the future.</span></span> <span data-ttu-id="77164-124">Psaní konfiguračních skriptů může být velmi obtížné, proto kvůli jako autor můžete zjednodušit sledování chyb, použít prostředek DSC Log ke sledování pokroku vaší konfigurace DSC analytického protokolu událostí.</span><span class="sxs-lookup"><span data-stu-id="77164-124">Writing configuration scripts can be tricky, so to make tracking errors easier as you author, use the DSC Log resource to track the progress of your configuration in the DSC Analytic event log.</span></span>

## <a name="where-are-dsc-event-logs"></a><span data-ttu-id="77164-125">Kde jsou protokoly událostí DSC?</span><span class="sxs-lookup"><span data-stu-id="77164-125">Where are DSC event logs?</span></span>

<span data-ttu-id="77164-126">V prohlížeči událostí jsou události DSC v: **Aplikace a služby protokoly/Microsoft/Windows/Desired State Configuration**</span><span class="sxs-lookup"><span data-stu-id="77164-126">In Event Viewer, DSC events are in: **Applications and Services Logs/Microsoft/Windows/Desired State Configuration**</span></span>

<span data-ttu-id="77164-127">Odpovídající rutiny prostředí PowerShell [Get-WinEvent](/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent), můžete spustit také zobrazit protokoly událostí:</span><span class="sxs-lookup"><span data-stu-id="77164-127">The corresponding PowerShell cmdlet, [Get-WinEvent](/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent), can also be run to view the event logs:</span></span>

```
PS C:\> Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"

   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
11/17/2014 10:27:23 PM        4102 Information      Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} :
```

<span data-ttu-id="77164-128">Jak uvádíme výš, je název vaší DSC primární protokolu **Microsoft -> Windows -> DSC** (jiné názvy protokolů v rámci Windows nejsou zobrazené pro zkrácení).</span><span class="sxs-lookup"><span data-stu-id="77164-128">As shown above, DSC's primary log name is **Microsoft->Windows->DSC** (other log names under Windows are not shown here for brevity).</span></span> <span data-ttu-id="77164-129">Primární název je připojeným k názvu kanálu k vytvoření názvu úplný protokol.</span><span class="sxs-lookup"><span data-stu-id="77164-129">The primary name is appended to the channel name to create the complete log name.</span></span> <span data-ttu-id="77164-130">Modul DSC zapíše hlavně na tři typy protokolů: [Provozní, analýzu a ladit protokoly](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc722404(v=ws.11)).</span><span class="sxs-lookup"><span data-stu-id="77164-130">The DSC engine writes mainly into three types of logs: [Operational, Analytic, and Debug logs](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc722404(v=ws.11)).</span></span> <span data-ttu-id="77164-131">Od analýzy a protokoly ladění jsou ve výchozím nastavení vypnuta, měli byste povolit v prohlížeči událostí.</span><span class="sxs-lookup"><span data-stu-id="77164-131">Since the analytic and debug logs are turned off by default, you should enable them in Event Viewer.</span></span> <span data-ttu-id="77164-132">Chcete-li to provést, otevřete Prohlížeč událostí tak, že zadáte zobrazit protokolu událostí Windows PowerShell nebo klikněte na tlačítko **Start** tlačítko, klikněte na tlačítko **ovládací panely**, klikněte na tlačítko **nástroje pro správu**a potom klikněte na tlačítko **Prohlížeč událostí**.</span><span class="sxs-lookup"><span data-stu-id="77164-132">To do this, open Event Viewer by typing Show-EventLog in Windows PowerShell; or, click the **Start** button, click **Control Panel**, click **Administrative Tools**, and then click **Event Viewer**.</span></span>
<span data-ttu-id="77164-133">Na **zobrazení** klikněte na tlačítko nabídky v prohlížeči událostí **zobrazit protokoly ladění a analýzu**.</span><span class="sxs-lookup"><span data-stu-id="77164-133">On the **View** menu in Event viewer, click **Show Analytic and Debug Logs**.</span></span> <span data-ttu-id="77164-134">Název protokolu analytického kanálu je **Microsoft-Windows-Dsc/analytické**, a je kanál ladění **Microsoft-Windows-Dsc/Debug**.</span><span class="sxs-lookup"><span data-stu-id="77164-134">The log name for the analytic channel is **Microsoft-Windows-Dsc/Analytic**, and the debug channel is **Microsoft-Windows-Dsc/Debug**.</span></span> <span data-ttu-id="77164-135">Můžete také použít [wevtutil](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc732848(v=ws.11)) nástroj a povolte je, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="77164-135">You could also use the [wevtutil](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc732848(v=ws.11)) utility to enable the logs, as shown in the following example.</span></span>

```powershell
wevtutil.exe set-log "Microsoft-Windows-Dsc/Analytic" /q:true /e:true
```

## <a name="what-do-dsc-logs-contain"></a><span data-ttu-id="77164-136">Co neobsahují DSC protokoly?</span><span class="sxs-lookup"><span data-stu-id="77164-136">What do DSC logs contain?</span></span>

<span data-ttu-id="77164-137">Protokoly DSC se rozdělit přes tři kanály protokolu na základě důležitosti zprávy.</span><span class="sxs-lookup"><span data-stu-id="77164-137">DSC logs are split over the three log channels based on the importance of the message.</span></span> <span data-ttu-id="77164-138">Operační protokol v DSC obsahuje všechny chybové zprávy a je možné identifikovat problém.</span><span class="sxs-lookup"><span data-stu-id="77164-138">The operational log in DSC contains all error messages, and can be used to identify a problem.</span></span> <span data-ttu-id="77164-139">Analytický protokol má větší objem událostí a zjistit, kde došlo k chybě.</span><span class="sxs-lookup"><span data-stu-id="77164-139">The analytic log has a higher volume of events, and can identify where error(s) occurred.</span></span> <span data-ttu-id="77164-140">Tento kanál obsahuje také podrobné zprávy (pokud existuje).</span><span class="sxs-lookup"><span data-stu-id="77164-140">This channel also contains verbose messages (if any).</span></span> <span data-ttu-id="77164-141">Protokol ladění obsahuje protokoly, které vám pomůžou pochopit, jak došlo k chybám.</span><span class="sxs-lookup"><span data-stu-id="77164-141">The debug log contains logs that can help you understand how the errors occurred.</span></span> <span data-ttu-id="77164-142">Zprávy o událostech DSC strukturovány tak, aby všechny zprávy událostí začne s ID úlohy, který jedinečně reprezentuje operaci DSC.</span><span class="sxs-lookup"><span data-stu-id="77164-142">DSC event messages are structured such that every event message begins with a job ID that uniquely represents a DSC operation.</span></span> <span data-ttu-id="77164-143">Následující příklad se pokusí získat zprávu od první událost, která je zaznamenána do protokolu provozní DSC.</span><span class="sxs-lookup"><span data-stu-id="77164-143">The example below attempts to obtain the message from the first event logged into the operational DSC log.</span></span>

```powershell
PS C:\> $AllDscOpEvents = Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
PS C:\> $FirstOperationalEvent = $AllDscOpEvents[0]
PS C:\> $FirstOperationalEvent.Message
Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} :
Consistency engine was run successfully.
```

<span data-ttu-id="77164-144">DSC události jsou protokolovány v konkrétní strukturu, která umožňuje uživateli pro agregaci událostí z jednoho projektu DSC.</span><span class="sxs-lookup"><span data-stu-id="77164-144">DSC events are logged in a particular structure that enables the user to aggregate events from one DSC job.</span></span> <span data-ttu-id="77164-145">Struktura je následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="77164-145">The structure is as follows:</span></span>

```
Job ID : <Guid>
<Event Message>
```

## <a name="gathering-events-from-a-single-dsc-operation"></a><span data-ttu-id="77164-146">Shromažďování událostí v rámci jedné operace DSC</span><span class="sxs-lookup"><span data-stu-id="77164-146">Gathering events from a single DSC operation</span></span>

<span data-ttu-id="77164-147">Protokoly událostí DSC obsahovat události generované modulem různé operace DSC.</span><span class="sxs-lookup"><span data-stu-id="77164-147">DSC event logs contain events generated by various DSC operations.</span></span> <span data-ttu-id="77164-148">Ale obvykle budete s detaily zajímá jenom jeden konkrétní operace.</span><span class="sxs-lookup"><span data-stu-id="77164-148">However, you'll usually be concerned with the detail about just one particular operation.</span></span> <span data-ttu-id="77164-149">Všechny protokoly DSC můžete seskupit podle vlastnosti ID úlohy, které jsou jedinečné pro každé operace DSC.</span><span class="sxs-lookup"><span data-stu-id="77164-149">All DSC logs can be grouped by the job ID property that is unique for every DSC operation.</span></span> <span data-ttu-id="77164-150">ID úlohy se zobrazí jako první hodnota vlastnosti ve všech událostí DSC.</span><span class="sxs-lookup"><span data-stu-id="77164-150">The job ID is displayed as the first property value in all DSC events.</span></span> <span data-ttu-id="77164-151">Následující postup vysvětluje, jak k shromažďování všech událostí ve struktuře seskupených pole.</span><span class="sxs-lookup"><span data-stu-id="77164-151">The following steps explain how to accumulate all events in a grouped array structure.</span></span>

```powershell
<##########################################################################
 Step 1 : Enable analytic and debug DSC channels (Operational channel is enabled by default)
###########################################################################>

wevtutil.exe set-log "Microsoft-Windows-Dsc/Analytic" /q:true /e:true
wevtutil.exe set-log "Microsoft-Windows-Dsc/Debug" /q:True /e:true

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

<span data-ttu-id="77164-152">Tady, proměnná `$SeparateDscOperations` obsahuje protokoly, které jsou seskupeny podle ID úloh.</span><span class="sxs-lookup"><span data-stu-id="77164-152">Here, the variable `$SeparateDscOperations` contains logs grouped by the job IDs.</span></span> <span data-ttu-id="77164-153">Každý prvek pole této proměnné představuje skupinu události zapsané podle jiné operace DSC, povolení přístupu na další informace o protokolech.</span><span class="sxs-lookup"><span data-stu-id="77164-153">Each array element of this variable represents a group of events logged by a different DSC operation, allowing access to more information about the logs.</span></span>

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

<span data-ttu-id="77164-154">Můžete extrahovat data v proměnné `$SeparateDscOperations` pomocí [Where-Object](/powershell/module/microsoft.powershell.core/where-object).</span><span class="sxs-lookup"><span data-stu-id="77164-154">You can extract the data in the variable `$SeparateDscOperations` using [Where-Object](/powershell/module/microsoft.powershell.core/where-object).</span></span> <span data-ttu-id="77164-155">Níže jsou pět scénáře, ve kterých můžete extrahovat data pro řešení potíží s DSC:</span><span class="sxs-lookup"><span data-stu-id="77164-155">Following are five scenarios in which you might want to extract data for troubleshooting DSC:</span></span>

### <a name="1-operations-failures"></a><span data-ttu-id="77164-156">1: Selhání operací</span><span class="sxs-lookup"><span data-stu-id="77164-156">1: Operations failures</span></span>

<span data-ttu-id="77164-157">Všechny události mají [úrovně závažnosti](/windows/desktop/WES/defining-severity-levels).</span><span class="sxs-lookup"><span data-stu-id="77164-157">All events have [severity levels](/windows/desktop/WES/defining-severity-levels).</span></span> <span data-ttu-id="77164-158">Tyto informace slouží k identifikaci chybové události:</span><span class="sxs-lookup"><span data-stu-id="77164-158">This information can be used to identify the error events:</span></span>

```
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.LevelDisplayName -contains "Error"}

Count Name                      Group
----- ----                      -----
   38 {5BCA8BE7-5BB6-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
```

### <a name="2-details-of-operations-run-in-the-last-half-hour"></a><span data-ttu-id="77164-159">2: Podrobnosti o spuštění v poslední půlhodiny operací</span><span class="sxs-lookup"><span data-stu-id="77164-159">2: Details of operations run in the last half hour</span></span>

<span data-ttu-id="77164-160">`TimeCreated`, vlastnost všech událostí Windows uvádí čas vytvoření události.</span><span class="sxs-lookup"><span data-stu-id="77164-160">`TimeCreated`, a property of every Windows event, states the time the event was created.</span></span> <span data-ttu-id="77164-161">Porovnání s objektem konkrétní datum a čas tato vlastnost slouží k filtrování všechny události:</span><span class="sxs-lookup"><span data-stu-id="77164-161">Comparing this property with a particular date/time object can be used to filter all events:</span></span>

```powershell
PS C:\> $DateLatest = (Get-Date).AddMinutes(-30)
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.TimeCreated -gt $DateLatest}

Count Name                      Group
----- ----                      -----
    1 {6CEC5B09-5BB0-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord}
```

### <a name="3-messages-from-the-latest-operation"></a><span data-ttu-id="77164-162">3: Zprávy od poslední operace</span><span class="sxs-lookup"><span data-stu-id="77164-162">3: Messages from the latest operation</span></span>

<span data-ttu-id="77164-163">Nejnovější operace je uložen v první index pole skupiny `$SeparateDscOperations`.</span><span class="sxs-lookup"><span data-stu-id="77164-163">The latest operation is stored in the first index of the array group `$SeparateDscOperations`.</span></span>
<span data-ttu-id="77164-164">Dotazování skupiny zpráv pro index 0, vrátí se všechny zprávy o poslední operaci:</span><span class="sxs-lookup"><span data-stu-id="77164-164">Querying the group's messages for index 0 returns all messages for the latest operation:</span></span>

```powershell
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

### <a name="4-error-messages-logged-for-recent-failed-operations"></a><span data-ttu-id="77164-165">4: Chybové zprávy pro poslední neúspěšné operace</span><span class="sxs-lookup"><span data-stu-id="77164-165">4: Error messages logged for recent failed operations</span></span>

<span data-ttu-id="77164-166">`$SeparateDscOperations[0].Group` obsahuje sadu událostí pro poslední operaci.</span><span class="sxs-lookup"><span data-stu-id="77164-166">`$SeparateDscOperations[0].Group` contains a set of events for the latest operation.</span></span> <span data-ttu-id="77164-167">Spustit `Where-Object` rutiny filtrovat události podle jejich úrovně zobrazovaného jména.</span><span class="sxs-lookup"><span data-stu-id="77164-167">Run the `Where-Object` cmdlet to filter the events based on their level display name.</span></span> <span data-ttu-id="77164-168">Výsledky jsou uloženy v `$myFailedEvent` proměnné, která může být dále odebrán zobrazíte zpráva o události:</span><span class="sxs-lookup"><span data-stu-id="77164-168">Results are stored in the `$myFailedEvent` variable, which can be further dissected to get the event message:</span></span>

```powershell
PS C:\> $myFailedEvent = ($SeparateDscOperations[0].Group | Where-Object {$_.LevelDisplayName -eq "Error"})

PS C:\> $myFailedEvent.Message

Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} :
DSC Engine Error :
 Error Message Current configuration does not exist. Execute Start-DscConfiguration command with -Path pa
rameter to specify a configuration file and create a current configuration first.
Error Code : 1
```

### <a name="5-all-events-generated-for-a-particular-job-id"></a><span data-ttu-id="77164-169">5: Všechny události vytvořené pro konkrétní úlohy ID.</span><span class="sxs-lookup"><span data-stu-id="77164-169">5: All events generated for a particular job ID.</span></span>

<span data-ttu-id="77164-170">`$SeparateDscOperations` je pole skupin, z nichž každá má název jako úlohy jedinečné ID.</span><span class="sxs-lookup"><span data-stu-id="77164-170">`$SeparateDscOperations` is an array of groups, each of which has the name as the unique job ID.</span></span> <span data-ttu-id="77164-171">Spuštěním `Where-Object` rutiny, můžete extrahovat těchto skupin události, které mají ID konkrétní úlohy:</span><span class="sxs-lookup"><span data-stu-id="77164-171">By running the `Where-Object` cmdlet, you can extract those groups of events that have a particular job ID:</span></span>

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

## <a name="using-xdscdiagnostics-to-analyze-dsc-logs"></a><span data-ttu-id="77164-172">Použití xDscDiagnostics k analýze DSC protokoly</span><span class="sxs-lookup"><span data-stu-id="77164-172">Using xDscDiagnostics to analyze DSC logs</span></span>

<span data-ttu-id="77164-173">**xDscDiagnostics** je modul Powershellu, které obsahuje několik funkcí, které vám mohou pomoci analýza selhání DSC na svém počítači.</span><span class="sxs-lookup"><span data-stu-id="77164-173">**xDscDiagnostics** is a PowerShell module that consists of several functions that can help analyze DSC failures on your machine.</span></span> <span data-ttu-id="77164-174">Tyto funkce můžete identifikovat všechny místní akce z poslední DSC operace nebo události DSC na vzdálených počítačích (se platné přihlašovací údaje).</span><span class="sxs-lookup"><span data-stu-id="77164-174">These functions can help you identify all local events from past DSC operations, or DSC events on remote computers (with valid credentials).</span></span> <span data-ttu-id="77164-175">Termín DSC operace tady, se používá k definování jeden jedinečný spuštění DSC od jeho začátku jeho ukončení.</span><span class="sxs-lookup"><span data-stu-id="77164-175">Here, the term DSC operation is used to define a single unique DSC execution from its start to its end.</span></span> <span data-ttu-id="77164-176">Například `Test-DscConfiguration` by samostatné operaci DSC.</span><span class="sxs-lookup"><span data-stu-id="77164-176">For example, `Test-DscConfiguration` would be a separate DSC operation.</span></span> <span data-ttu-id="77164-177">Podobně, každý další rutiny v DSC (například `Get-DscConfiguration`, `Start-DscConfiguration`atd) každý nelze identifikovat jako samostatné operace DSC.</span><span class="sxs-lookup"><span data-stu-id="77164-177">Similarly, every other cmdlet in DSC (such as `Get-DscConfiguration`, `Start-DscConfiguration`, etc.) could each be identified as separate DSC operations.</span></span> <span data-ttu-id="77164-178">Funkce jsou vysvětleny v [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics).</span><span class="sxs-lookup"><span data-stu-id="77164-178">The functions are explained at [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics).</span></span> <span data-ttu-id="77164-179">Není k dispozici nápověda spuštěním `Get-Help <cmdlet name>`.</span><span class="sxs-lookup"><span data-stu-id="77164-179">Help is available by running `Get-Help <cmdlet name>`.</span></span>

### <a name="getting-details-of-dsc-operations"></a><span data-ttu-id="77164-180">Získávání podrobností operací DSC</span><span class="sxs-lookup"><span data-stu-id="77164-180">Getting details of DSC operations</span></span>

<span data-ttu-id="77164-181">`Get-xDscOperation` Funkce vám umožní najít výsledky operací DSC, které běží na jeden nebo více počítačů a vrátí objekt, který obsahuje kolekci událostí produkovaný každou operaci DSC.</span><span class="sxs-lookup"><span data-stu-id="77164-181">The `Get-xDscOperation` function lets you find the results of the DSC operations that run on one or multiple computers, and returns an object that contains the collection of events produced by each DSC operation.</span></span> <span data-ttu-id="77164-182">V následující výstup například tři příkazy byly spuštěny.</span><span class="sxs-lookup"><span data-stu-id="77164-182">For example, in the following output, three commands were run.</span></span> <span data-ttu-id="77164-183">Předaný první a druhé dvě selhala.</span><span class="sxs-lookup"><span data-stu-id="77164-183">The first one passed, and the other two failed.</span></span> <span data-ttu-id="77164-184">Tyto výsledky jsou shrnuty v rámci výstupu `Get-xDscOperation`.</span><span class="sxs-lookup"><span data-stu-id="77164-184">These results are summarized in the output of `Get-xDscOperation`.</span></span>

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation

ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents
------------   ---------- -----------           ------   -----                                 ---------
SRV1   1          6/23/2016 9:37:52 AM  Failure  9701aadf-395e-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   2          6/23/2016 9:36:54 AM  Failure  7e8e2d6e-395c-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   3          6/23/2016 9:36:54 AM  Success  af72c6aa-3960-11e6-9165-00155d390509  {@{Message=Operati...
```

<span data-ttu-id="77164-185">Můžete také určit, který má pouze výsledky pro poslední operace s použitím `Newest` parametr:</span><span class="sxs-lookup"><span data-stu-id="77164-185">You can also specify that you want only results for the most recent operations by using the `Newest` parameter:</span></span>

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

### <a name="getting-details-of-dsc-events"></a><span data-ttu-id="77164-186">Získávání podrobností o události DSC</span><span class="sxs-lookup"><span data-stu-id="77164-186">Getting details of DSC events</span></span>

<span data-ttu-id="77164-187">`Trace-xDscOperation` Rutina vrátí objekt, který obsahuje kolekci událostí, jejich typy událostí, a výstupní zprávy generované určitou operaci DSC.</span><span class="sxs-lookup"><span data-stu-id="77164-187">The `Trace-xDscOperation` cmdlet returns an object containing a collection of events, their event types, and the message output generated from a particular DSC operation.</span></span> <span data-ttu-id="77164-188">Obvykle, když najdete selhání v některém z operací pomocí `Get-xDscOperation`, by trasování činnosti s cílem zjistit, která z události způsobila chybu.</span><span class="sxs-lookup"><span data-stu-id="77164-188">Typically, when you find a failure in any of the operations using `Get-xDscOperation`, you would trace that operation to find out which of the events caused a failure.</span></span>

<span data-ttu-id="77164-189">Použití `SequenceID` parametr získat události pro konkrétní operaci pro určitý počítač.</span><span class="sxs-lookup"><span data-stu-id="77164-189">Use the `SequenceID` parameter to get the events for a specific operation for a specific computer.</span></span>
<span data-ttu-id="77164-190">Pokud zadáte například `SequenceID` 9, `Trace-xDscOperaion` získat trasování pro operace DSC, která byla 9 od poslední operace:</span><span class="sxs-lookup"><span data-stu-id="77164-190">For example, if you specify a `SequenceID` of 9, `Trace-xDscOperaion` get the trace for the DSC operation that was 9th from the last operation:</span></span>

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

<span data-ttu-id="77164-191">Předání **GUID** přiřazené k určité operace DSC (vrácené `Get-xDscOperation` rutiny) zobrazíte podrobnosti o události pro tuto operaci DSC:</span><span class="sxs-lookup"><span data-stu-id="77164-191">Pass the **GUID** assigned to a specific DSC operation (as returned by the `Get-xDscOperation` cmdlet) to get the event details for that DSC operation:</span></span>

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

<span data-ttu-id="77164-192">Všimněte si, že od té doby `Trace-xDscOperation` agreguje události z analýzy, ladění a provozní protokoly, vás vyzve k povolení těchto protokolů, jak je popsáno výše.</span><span class="sxs-lookup"><span data-stu-id="77164-192">Note that, since `Trace-xDscOperation` aggregates events from the Analytic, Debug, and Operational logs, it will prompt you to enable these logs as described above.</span></span>

<span data-ttu-id="77164-193">Alternativně můžete shromáždit informace o událostech prostřednictvím ukládání výstupu `Trace-xDscOperation` do proměnné.</span><span class="sxs-lookup"><span data-stu-id="77164-193">Alternately, you can gather information on the events by saving the output of `Trace-xDscOperation` into a variable.</span></span> <span data-ttu-id="77164-194">Pokud chcete zobrazit všechny události pro určitou operaci DSC můžete použít následující příkazy.</span><span class="sxs-lookup"><span data-stu-id="77164-194">You can use the following commands to display all the events for a particular DSC operation.</span></span>

```powershell
PS C:\DiagnosticsTest> $Trace = Trace-xDscOperation -SequenceID 4

PS C:\DiagnosticsTest> $Trace.Event
```

<span data-ttu-id="77164-195">Zobrazí se stejné výsledky jako `Get-WinEvent` rutiny, jako je například následující výstup:</span><span class="sxs-lookup"><span data-stu-id="77164-195">This will display the same results as the `Get-WinEvent` cmdlet, such as in the output below:</span></span>

```output
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

<span data-ttu-id="77164-196">V ideálním případě byste nejdřív použili `Get-xDscOperation` na seznam posledních několika DSC konfigurace běží na vašich počítačích.</span><span class="sxs-lookup"><span data-stu-id="77164-196">Ideally, you would first use `Get-xDscOperation` to list out the last few DSC configuration runs on your machines.</span></span> <span data-ttu-id="77164-197">Při tomto postupu můžete prozkoumat všechny najednou (pomocí jeho SequenceID nebo JobID) s `Trace-xDscOperation` zjistit, co jste na pozadí.</span><span class="sxs-lookup"><span data-stu-id="77164-197">Following this, you can examine any single operation (using its SequenceID or JobID) with `Trace-xDscOperation` to discover what it did behind the scenes.</span></span>

### <a name="getting-events-for-a-remote-computer"></a><span data-ttu-id="77164-198">Získat události na vzdálený počítač</span><span class="sxs-lookup"><span data-stu-id="77164-198">Getting events for a remote computer</span></span>

<span data-ttu-id="77164-199">Použití `ComputerName` parametr `Trace-xDscOperation` rutiny pro získání podrobností událostí na vzdáleném počítači.</span><span class="sxs-lookup"><span data-stu-id="77164-199">Use the `ComputerName` parameter of the `Trace-xDscOperation` cmdlet to get the event details on a remote computer.</span></span> <span data-ttu-id="77164-200">Předtím, než můžete provést, je nutné vytvořit pravidlo brány firewall pro povolení vzdálené správy na vzdáleném počítači:</span><span class="sxs-lookup"><span data-stu-id="77164-200">Before you can do this, you have to create a firewall rule to allow remote administration on the remote computer:</span></span>

```powershell
New-NetFirewallRule -Name "Service RemoteAdmin" -DisplayName "Remote" -Action Allow
```

<span data-ttu-id="77164-201">Nyní zadáte tento počítač při volání funkce vaše `Trace-xDscOperation`:</span><span class="sxs-lookup"><span data-stu-id="77164-201">Now you can specify that computer in your call to `Trace-xDscOperation`:</span></span>

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

## <a name="my-resources-wont-update-how-to-reset-the-cache"></a><span data-ttu-id="77164-202">Moje prostředky nebude aktualizovat: Resetování mezipaměti</span><span class="sxs-lookup"><span data-stu-id="77164-202">My resources won't update: How to reset the cache</span></span>

<span data-ttu-id="77164-203">Modul DSC prostředky, které jsou implementovány jako modul Powershellu pro účely efektivitu ukládá do mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="77164-203">The DSC engine caches resources implemented as a PowerShell module for efficiency purposes.</span></span>
<span data-ttu-id="77164-204">Nicméně to může způsobit problémy při vytváření prostředku a otestujete ji současně, protože DSC načte verze uložené v mezipaměti až po restartování procesu.</span><span class="sxs-lookup"><span data-stu-id="77164-204">However, this can cause problems when you are authoring a resource and testing it simultaneously because DSC will load the cached version until the process is restarted.</span></span> <span data-ttu-id="77164-205">Jediný způsob, jak provést DSC načíst novější verze je explicitně ukončení procesu, který je hostitelem modulu DSC.</span><span class="sxs-lookup"><span data-stu-id="77164-205">The only way to make DSC load the newer version is to explicitly kill the process hosting the DSC engine.</span></span>

<span data-ttu-id="77164-206">Podobně, když spustíte `Start-DscConfiguration`, po přidání a úpravy vlastní prostředek, pravděpodobně nebude spuštěna úpravy, není-li nebo, dokud nebude počítač restartován.</span><span class="sxs-lookup"><span data-stu-id="77164-206">Similarly, when you run `Start-DscConfiguration`, after adding and modifying a custom resource, the modification may not execute unless, or until, the computer is rebooted.</span></span> <span data-ttu-id="77164-207">Je to proto DSC běží v hostitelském procesu zprostředkovatele rozhraní WMI (WmiPrvSE) a existují obvykle velký počet instancí WmiPrvSE najednou spuštěna.</span><span class="sxs-lookup"><span data-stu-id="77164-207">This is because DSC runs in the WMI Provider Host Process (WmiPrvSE), and usually, there are many instances of WmiPrvSE running at once.</span></span> <span data-ttu-id="77164-208">Když restartujete, restartování hostitelského procesu a nevymažete mezipaměť.</span><span class="sxs-lookup"><span data-stu-id="77164-208">When you reboot, the host process is restarted and the cache is cleared.</span></span>

<span data-ttu-id="77164-209">Úspěšně recyklovat konfiguraci a vymažte její mezipaměť bez nutnosti restartování, musíte zastavit a poté restartujte hostitelský proces.</span><span class="sxs-lookup"><span data-stu-id="77164-209">To successfully recycle the configuration and clear the cache without rebooting, you must stop and then restart the host process.</span></span> <span data-ttu-id="77164-210">To můžete udělat na na základě instancí, kterým Identifikujte proces, zastavte ji a restartujte ji.</span><span class="sxs-lookup"><span data-stu-id="77164-210">This can be done on a per instance basis, whereby you identify the process, stop it, and restart it.</span></span> <span data-ttu-id="77164-211">Nebo můžete použít `DebugMode`, jak je znázorněno níže, k opětovnému načtení prostředků DSC Powershellu.</span><span class="sxs-lookup"><span data-stu-id="77164-211">Or, you can use `DebugMode`, as demonstrated below, to reload the PowerShell DSC resource.</span></span>

<span data-ttu-id="77164-212">K identifikaci, který proces je hostitelem modulu DSC a zastavte ji na na základě instancí, můžete vytvořit seznam ID procesu sady WmiPrvSE, který je hostitelem modulu DSC.</span><span class="sxs-lookup"><span data-stu-id="77164-212">To identify which process is hosting the DSC engine and stop it on a per instance basis, you can list the process ID of the WmiPrvSE which is hosting the DSC engine.</span></span> <span data-ttu-id="77164-213">Poté, aktualizovat poskytovatele, zastavte WmiPrvSE procesu pomocí níže uvedených příkazů a potom spusťte **Start-DscConfiguration** znovu.</span><span class="sxs-lookup"><span data-stu-id="77164-213">Then, to update the provider, stop the WmiPrvSE process using the commands below, and then run **Start-DscConfiguration** again.</span></span>

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

## <a name="using-debugmode"></a><span data-ttu-id="77164-214">Režim DebugMode pomocí</span><span class="sxs-lookup"><span data-stu-id="77164-214">Using DebugMode</span></span>

<span data-ttu-id="77164-215">Můžete nakonfigurovat DSC místní Configuration Manageru (LCM) používat `DebugMode` a vždy vymažte mezipaměť při restartování hostitelského procesu.</span><span class="sxs-lookup"><span data-stu-id="77164-215">You can configure the DSC Local Configuration Manager (LCM) to use `DebugMode` to always clear the cache when the host process is restarted.</span></span> <span data-ttu-id="77164-216">Pokud je nastavena na **TRUE**, způsobí, že modul, aby vždy znovu načíst prostředek DSC Powershellu.</span><span class="sxs-lookup"><span data-stu-id="77164-216">When set to **TRUE**, it causes the engine to always reload the PowerShell DSC resource.</span></span> <span data-ttu-id="77164-217">Po dokončení zápisu váš prostředek, můžete ho nastavit zpět **FALSE** a modul bude používat pro své chování ukládání do mezipaměti moduly.</span><span class="sxs-lookup"><span data-stu-id="77164-217">Once you are done writing your resource, you can set it back to **FALSE** and the engine will revert to its behavior of caching the modules.</span></span>

<span data-ttu-id="77164-218">Tady je ukázka zobrazíte jak `DebugMode` můžete automaticky aktualizovat mezipaměť.</span><span class="sxs-lookup"><span data-stu-id="77164-218">Following is a demonstration to show how `DebugMode` can automatically refresh the cache.</span></span> <span data-ttu-id="77164-219">Nejprve Podívejme se na výchozí konfigurace:</span><span class="sxs-lookup"><span data-stu-id="77164-219">First, let's look at the default configuration:</span></span>

```powershell
PS C:\> Get-DscLocalConfigurationManager
```

```output
AllowModuleOverwrite           : False
CertificateID                  :
ConfigurationID                :
ConfigurationMode              : ApplyAndMonitor
ConfigurationModeFrequencyMins : 30
Credential                     :
DebugMode                      : {None}
DownloadManagerCustomData      :
DownloadManagerName            :
LocalConfigurationManagerState : Ready
RebootNodeIfNeeded             : False
RefreshFrequencyMins           : 15
RefreshMode                    : PUSH
PSComputerName                 :
```

<span data-ttu-id="77164-220">Vidíte, že `DebugMode` je nastavena na **"None"**.</span><span class="sxs-lookup"><span data-stu-id="77164-220">You can see that `DebugMode` is set to **"None"**.</span></span>

<span data-ttu-id="77164-221">Nastavit `DebugMode` ukázku, použijte následující prostředek prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="77164-221">To set up the `DebugMode` demonstration, use the following PowerShell resource:</span></span>

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

<span data-ttu-id="77164-222">Nyní, vytváření konfigurace pomocí výše uvedených prostředků volá `TestProviderDebugMode`:</span><span class="sxs-lookup"><span data-stu-id="77164-222">Now, author a configuration using the above resource called `TestProviderDebugMode`:</span></span>

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

<span data-ttu-id="77164-223">Uvidíte, že obsah souboru: `$env:SystemDrive\OutputFromTestProviderDebugMode.txt` je **1**.</span><span class="sxs-lookup"><span data-stu-id="77164-223">You will see that the contents of file: `$env:SystemDrive\OutputFromTestProviderDebugMode.txt` is **1**.</span></span>

<span data-ttu-id="77164-224">Nyní aktualizace zprostředkovatele kódu pomocí následujícího skriptu:</span><span class="sxs-lookup"><span data-stu-id="77164-224">Now, update the provider code using the following script:</span></span>

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

<span data-ttu-id="77164-225">Tento skript generuje náhodné číslo a odpovídajícím způsobem aktualizuje zprostředkovatele kódu.</span><span class="sxs-lookup"><span data-stu-id="77164-225">This script generates a random number and updates the provider code accordingly.</span></span> <span data-ttu-id="77164-226">S `DebugMode` nastavena na hodnotu false, obsah souboru "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**" se nikdy změněn.</span><span class="sxs-lookup"><span data-stu-id="77164-226">With `DebugMode` set to false, the contents of the file "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**" are never changed.</span></span>

<span data-ttu-id="77164-227">Nyní nastavte `DebugMode` k **"ForceModuleImport"** v konfigurační skript:</span><span class="sxs-lookup"><span data-stu-id="77164-227">Now, set `DebugMode` to **"ForceModuleImport"** in your configuration script:</span></span>

```powershell
LocalConfigurationManager
{
    DebugMode = "ForceModuleImport"
}
```

<span data-ttu-id="77164-228">Když znovu spustíte výše uvedené skript, uvidíte, že obsah souboru se liší pokaždé, když.</span><span class="sxs-lookup"><span data-stu-id="77164-228">When you run the above script again, you will see that the content of the file is different every time.</span></span> <span data-ttu-id="77164-229">(Můžete spustit `Get-DscConfiguration` tak zkontrolovat, že).</span><span class="sxs-lookup"><span data-stu-id="77164-229">(You can run `Get-DscConfiguration` to check it).</span></span> <span data-ttu-id="77164-230">Níže je výsledek dvě další spuštění (výsledky mohou lišit při spuštění skriptu):</span><span class="sxs-lookup"><span data-stu-id="77164-230">Below is the result of two additional runs (your results may be different when you run the script):</span></span>

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

## <a name="see-also"></a><span data-ttu-id="77164-231">Viz také</span><span class="sxs-lookup"><span data-stu-id="77164-231">See Also</span></span>

### <a name="concepts"></a><span data-ttu-id="77164-232">Koncepty</span><span class="sxs-lookup"><span data-stu-id="77164-232">Concepts</span></span>

- [<span data-ttu-id="77164-233">Vlastní Windows PowerShell Desired State Configuration prostředky sestavení</span><span class="sxs-lookup"><span data-stu-id="77164-233">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](../resources/authoringResource.md)

### <a name="other-resources"></a><span data-ttu-id="77164-234">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="77164-234">Other Resources</span></span>

- [<span data-ttu-id="77164-235">Prostředí Windows PowerShell Desired State Configuration rutiny</span><span class="sxs-lookup"><span data-stu-id="77164-235">Windows PowerShell Desired State Configuration Cmdlets</span></span>](/powershell/module/psdesiredstateconfiguration/)
