---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Použití serveru sestav DSC
ms.openlocfilehash: 8647f80c311ee49a5cc4d57360472386e01b044e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403845"
---
# <a name="using-a-dsc-report-server"></a><span data-ttu-id="1f289-103">Použití serveru sestav DSC</span><span class="sxs-lookup"><span data-stu-id="1f289-103">Using a DSC report server</span></span>

<span data-ttu-id="1f289-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1f289-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f289-105">Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="1f289-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="1f289-106">Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="1f289-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>
>
> <span data-ttu-id="1f289-107">**Poznámka:** server sestav, které jsou popsané v tomto tématu není k dispozici v Powershellu 4.0.</span><span class="sxs-lookup"><span data-stu-id="1f289-107">**Note** The report server described in this topic is not available in PowerShell 4.0.</span></span>

<span data-ttu-id="1f289-108">Místní Configuration Manageru (LCM) uzlu můžete nakonfigurovat zasílání zpráv o informace o jeho stavu konfigurace na serveru vyžádané replikace, který může být dotazován načíst data.</span><span class="sxs-lookup"><span data-stu-id="1f289-108">The Local Configuration Manager (LCM) of a node can be configured to send reports about its configuration status to a pull server, which can then be queried to retrieve that data.</span></span> <span data-ttu-id="1f289-109">Pokaždé, když uzel zkontroluje a použije konfiguraci, odešle sestavy na server sestav.</span><span class="sxs-lookup"><span data-stu-id="1f289-109">Each time the node checks and applies a configuration, it sends a report to the report server.</span></span> <span data-ttu-id="1f289-110">Tyto sestavy jsou uloženy v databázi na serveru a může být načten voláním webové službě generování sestav.</span><span class="sxs-lookup"><span data-stu-id="1f289-110">These reports are stored in a database on the server, and can be retrieved by calling the reporting web service.</span></span> <span data-ttu-id="1f289-111">Každá sestava obsahuje informace, jako je konfigurace, které byly použity a určuje, zda jsou úspěšné, používá prostředky, všechny chyby, které byly vyvolány a časy zahájení a dokončení.</span><span class="sxs-lookup"><span data-stu-id="1f289-111">Each report contains information such as what configurations were applied and whether they succeeded, the resources used, any errors that were thrown, and start and finish times.</span></span>

## <a name="configuring-a-node-to-send-reports"></a><span data-ttu-id="1f289-112">Konfigurace uzlu zasílání zpráv</span><span class="sxs-lookup"><span data-stu-id="1f289-112">Configuring a node to send reports</span></span>

<span data-ttu-id="1f289-113">Zjistit uzel odesílání sestav na server pomocí **ReportServerWeb** blokovat do konfigurace LCM uzlu (informace o konfiguraci LCM najdete v tématu [konfigurace Local Configuration Manageru](../managing-nodes/metaConfig.md) ).</span><span class="sxs-lookup"><span data-stu-id="1f289-113">You tell a node to send reports to a server by using a **ReportServerWeb** block in the node's LCM configuration (for information about configuring the LCM, see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig.md)).</span></span> <span data-ttu-id="1f289-114">Server, ke kterému uzel odesílá sestavy musíte nastavit jako webového serveru vyžádané replikace (nelze odeslat sestavy do sdílené složky protokolu SMB).</span><span class="sxs-lookup"><span data-stu-id="1f289-114">The server to which the node sends reports must be set up as a web pull server (you cannot send reports to an SMB share).</span></span> <span data-ttu-id="1f289-115">Informace o nastavení serveru vyžádané replikace najdete v tématu [nastavení webového serveru vyžádané replikace DSC](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="1f289-115">For information about setting up a pull server, see [Setting up a DSC web pull server](pullServer.md).</span></span> <span data-ttu-id="1f289-116">Server sestav může být stejnou službu, ze kterého si vyžádá konfigurace uzlu a získá prostředky, nebo může být jiné služby.</span><span class="sxs-lookup"><span data-stu-id="1f289-116">The report server can be the same service from which the node pulls configurations and gets resources, or it can be a different service.</span></span>

<span data-ttu-id="1f289-117">V **ReportServerWeb** blok, můžete zadat adresu URL služby o přijetí změn a registrační klíč, který je známý k serveru.</span><span class="sxs-lookup"><span data-stu-id="1f289-117">In the **ReportServerWeb** block, you specify the URL of the pull service and a registration key that is known to the server.</span></span>

<span data-ttu-id="1f289-118">Následující konfigurace nakonfiguruje uzel o přijetí změn konfigurace z jedné služby a odesílat zprávy do služby na jiném serveru.</span><span class="sxs-lookup"><span data-stu-id="1f289-118">The following configuration configures a node to pull configurations from one service, and send reports to a service on a different server.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration ReportClientConfig
{
    Node localhost
    {
        Settings
        {
            RefreshMode          = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded   = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL          = 'https://CONTOSO-PULL:8080/PSDSCPullServer.svc'
            RegistrationKey    = 'bbb9778f-43f2-47de-b61e-a0daff474c6d'
            ConfigurationNames = @('ClientConfig')
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL               = 'http://CONTOSO-REPORT:8080/PSDSCReportServer.svc'
            RegistrationKey         = 'ba39daaa-96c5-4f2f-9149-f95c46460faa'
            AllowUnsecureConnection = $true
        }
    }
}

ReportClientConfig
```

<span data-ttu-id="1f289-119">Následující konfigurace nakonfiguruje uzel, který použijete jeden server pro konfigurace, prostředků a vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="1f289-119">The following configuration configures a node to use a single server for configurations, resources, and reporting.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfig
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }



        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfig
```

> [!NOTE]
> <span data-ttu-id="1f289-120">Můžete pojmenovat webové službě cokoliv, co chcete, při nastavení serveru vyžádané replikace, ale **ServerURL** vlastnost musí odpovídat názvu služby.</span><span class="sxs-lookup"><span data-stu-id="1f289-120">You can name the web service whatever you want when you set up a pull server, but the **ServerURL** property must match the service name.</span></span>

## <a name="getting-report-data"></a><span data-ttu-id="1f289-121">Načtení dat sestavy</span><span class="sxs-lookup"><span data-stu-id="1f289-121">Getting report data</span></span>

<span data-ttu-id="1f289-122">Zprávy zasílané na server vyžádané replikace jsou zadány do databáze na serveru.</span><span class="sxs-lookup"><span data-stu-id="1f289-122">Reports sent to the pull server are entered into a database on the server.</span></span> <span data-ttu-id="1f289-123">Sestavy jsou k dispozici prostřednictvím volání webové služby.</span><span class="sxs-lookup"><span data-stu-id="1f289-123">The reports are available through calls to the web service.</span></span> <span data-ttu-id="1f289-124">Pokud chcete načíst sestavy pro konkrétní uzel, odesláním požadavku HTTP k webové službě sestavy v následující podobě: `http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId='MyNodeAgentId')/Reports`</span><span class="sxs-lookup"><span data-stu-id="1f289-124">To retrieve reports for a specific node, send an HTTP request to the report web service in the following form: `http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId='MyNodeAgentId')/Reports`</span></span>
<span data-ttu-id="1f289-125">kde `MyNodeAgentId` je ID agenta uzlu, pro které chcete získat sestavy.</span><span class="sxs-lookup"><span data-stu-id="1f289-125">where `MyNodeAgentId` is the AgentId of the node for which you want to get reports.</span></span> <span data-ttu-id="1f289-126">ID agenta pro uzel můžete získat voláním [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) na tomto uzlu.</span><span class="sxs-lookup"><span data-stu-id="1f289-126">You can get the AgentID for a node by calling [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) on that node.</span></span>

<span data-ttu-id="1f289-127">Sestavy se vrátí jako pole objektů JSON.</span><span class="sxs-lookup"><span data-stu-id="1f289-127">The reports are returned as an array of JSON objects.</span></span>

<span data-ttu-id="1f289-128">Sestavy pro uzel, na kterém je spuštěn, vrátí se následující skript:</span><span class="sxs-lookup"><span data-stu-id="1f289-128">The following script returns the reports for the node on which it is run:</span></span>

```powershell
function GetReport
{
    param
    (
        $AgentId = "$((glcm).AgentId)", 
        $serviceURL = "http://CONTOSO-REPORT:8080/PSDSCPullServer.svc"
    )

    $requestUri = "$serviceURL/Nodes(AgentId= '$AgentId')/Reports"
    $request = Invoke-WebRequest -Uri $requestUri  -ContentType "application/json;odata=minimalmetadata;streaming=true;charset=utf-8" `
               -UseBasicParsing -Headers @{Accept = "application/json";ProtocolVersion = "2.0"} `
               -ErrorAction SilentlyContinue -ErrorVariable ev
    $object = ConvertFrom-Json $request.content
    return $object.value
}
```

## <a name="viewing-report-data"></a><span data-ttu-id="1f289-129">Zobrazení dat sestavy</span><span class="sxs-lookup"><span data-stu-id="1f289-129">Viewing report data</span></span>

<span data-ttu-id="1f289-130">Pokud jste nastavili proměnné na výsledek **GetReport** funkce, můžete zobrazit jednotlivá pole v elementu pole, která je vrácena:</span><span class="sxs-lookup"><span data-stu-id="1f289-130">If you set a variable to the result of the **GetReport** function, you can view the individual fields in an element of the array that is returned:</span></span>

```powershell
$reports = GetReport
$reports[1]
```

```output
JobId                : 019dfbe5-f99f-11e5-80c6-001dd8b8065c
OperationType        : Consistency
RefreshMode          : Pull
Status               : Success
ReportFormatVersion  : 2.0
ConfigurationVersion : 2.0.0
StartTime            : 04/03/2016 06:21:43
EndTime              : 04/03/2016 06:22:04
RebootRequested      : False
Errors               : {}
StatusData           : {{"StartDate":"2016-04-03T06:21:43.7220000-07:00","IPV6Addresses":["2001:4898:d8:f2f2:852b:b255:b071:283b","fe80::852b:b255:b071
                       :283b%12","::2000:0:0:0","::1","::2000:0:0:0"],"DurationInSeconds":"21","JobID":"{019DFBE5-F99F-11E5-80C6-001DD8B8065C}","Curren
                       tChecksum":"A7797571CB9C3AF4D74C39A0FDA11DAF33273349E1182385528FFC1E47151F7F","MetaData":"Author: configAuthor; Name:
                       Sample_ArchiveFirewall; Version: 2.0.0; GenerationDate: 04/01/2016 15:23:30; GenerationHost: CONTOSO-PullSrv;","RebootRequested":"False
                       ","Status":"Success","IPV4Addresses":["10.240.179.151","127.0.0.1"],"LCMVersion":"2.0","ResourcesNotInDesiredState":[{"SourceInf
                       o":"C:\\ReportTest\\Sample_xFirewall_AddFirewallRule.ps1::23::9::xFirewall","ModuleName":"xNetworking","DurationInSeconds":"8.785",
                       "InstanceName":"Firewall","StartDate":"2016-04-03T06:21:56.4650000-07:00","ResourceName":"xFirewall","ModuleVersion":"2.7.0.0","
                       RebootRequested":"False","ResourceId":"[xFirewall]Firewall","ConfigurationName":"Sample_ArchiveFirewall","InDesiredState":"False
                       "}],"NumberOfResources":"2","Type":"Consistency","HostName":"CONTOSO-PULLCLI","ResourcesInDesiredState":[{"SourceInfo":"C:\\ReportTest\\Sample_xFirewall_AddFirewallRule.ps1::16::9::Archive","ModuleName":"PSDesiredStateConfiguration","DurationInSeconds":"1.848",
                       "InstanceName":"ArchiveExample","StartDate":"2016-04-03T06:21:56.4650000-07:00","ResourceName":"Archive","ModuleVersion":"1.1","
                       RebootRequested":"False","ResourceId":"[Archive]ArchiveExample","ConfigurationName":"Sample_ArchiveFirewall","InDesiredState":"T
                       rue"}],"MACAddresses":["00-1D-D8-B8-06-5C","00-00-00-00-00-00-00-E0"],"MetaConfiguration":{"AgentId":"52DA826D-00DE-4166-8ACB-73F2B46A7E00",
                       "ConfigurationDownloadManagers":[{"SourceInfo":"C:\\ReportTest\\LCMConfig.ps1::14::9::ConfigurationRepositoryWeb","A
                       llowUnsecureConnection":"True","ServerURL":"http://CONTOSO-PullSrv:8080/PSDSCPullServer.svc","RegistrationKey":"","ResourceId":"[Config
                       urationRepositoryWeb]CONTOSO-PullSrv","ConfigurationNames":["ClientConfig"]}],"ActionAfterReboot":"ContinueConfiguration","LCMCo
                       mpatibleVersions":["1.0","2.0"],"LCMState":"Idle","ResourceModuleManagers":[],"ReportManagers":[{"AllowUnsecureConnection":"True
                       ","RegistrationKey":"","ServerURL":"http://CONTOSO-PullSrv:8080/PSDSCPullServer.svc","ResourceId":"[ReportServerWeb]CONTOSO-PullSrv","S
                       ourceInfo":"C:\\ReportTest\\LCMConfig.ps1::24::9::ReportServerWeb"}],"StatusRetentionTimeInDays":"10","LCMVersion":"2.0","Config
                       urationMode":"ApplyAndMonitor","RefreshFrequencyMins":"30","RebootNodeIfNeeded":"True","RefreshMode":"Pull","DebugMode":["NONE"]
                       ,"LCMStateDetail":"","AllowModuleOverwrite":"False","ConfigurationModeFrequencyMins":"15"},"Locale":"en-US","Mode":"Pull"}}
AdditionalData       : {}
```

<span data-ttu-id="1f289-131">Ve výchozím nastavení, sestavy jsou seřazeny podle **JobID**.</span><span class="sxs-lookup"><span data-stu-id="1f289-131">By default, the reports are sorted by **JobID**.</span></span> <span data-ttu-id="1f289-132">Pokud chcete získat nejnovější sestavy, můžete seřaďte sestavy podle sestupných **StartTime** vlastnost a potom získat první prvek pole:</span><span class="sxs-lookup"><span data-stu-id="1f289-132">To get the most recent report, you can sort the reports by descending **StartTime** property, and then get the first element of the array:</span></span>

```powershell
$reportsByStartTime = $reports | Sort-Object {$_."StartTime" -as [DateTime] } -Descending
$reportMostRecent = $reportsByStartTime[0]
```

<span data-ttu-id="1f289-133">Všimněte si, **StatusData** vlastnosti je objekt s číslem vlastností.</span><span class="sxs-lookup"><span data-stu-id="1f289-133">Notice that the **StatusData** property is an object with a number of properties.</span></span> <span data-ttu-id="1f289-134">To je, kde velká část generování sestav dat je.</span><span class="sxs-lookup"><span data-stu-id="1f289-134">This is where much of the reporting data is.</span></span> <span data-ttu-id="1f289-135">Podívejme se na jednotlivé položky **StatusData** vlastnost nejnovější sestavy:</span><span class="sxs-lookup"><span data-stu-id="1f289-135">Let's look at the individual fields of the **StatusData** property for the most recent report:</span></span>

```powershell
$statusData = $reportMostRecent.StatusData | ConvertFrom-Json
$statusData
```

```output
StartDate                  : 2016-04-04T11:21:41.2990000-07:00
IPV6Addresses              : {2001:4898:d8:f2f2:852b:b255:b071:283b, fe80::852b:b255:b071:283b%12, ::2000:0:0:0, ::1...}
DurationInSeconds          : 25
JobID                      : {135D230E-FA92-11E5-80C6-001DD8B8065C}
CurrentChecksum            : A7797571CB9C3AF4D74C39A0FDA11DAF33273349E1182385528FFC1E47151F7F
MetaData                   : Author: configAuthor; Name: Sample_ArchiveFirewall; Version: 2.0.0; GenerationDate: 04/01/2016 15:23:30; GenerationHost:
                             CONTOSO-PullSrv;
RebootRequested            : False
Status                     : Success
IPV4Addresses              : {10.240.179.151, 127.0.0.1}
LCMVersion                 : 2.0
ResourcesNotInDesiredState : {@{SourceInfo=C:\ReportTest\Sample_xFirewall_AddFirewallRule.ps1::23::9::xFirewall; ModuleName=xNetworking;
                             DurationInSeconds=10.725; InstanceName=Firewall; StartDate=2016-04-04T11:21:55.7200000-07:00; ResourceName=xFirewall;
                             ModuleVersion=2.7.0.0; RebootRequested=False; ResourceId=[xFirewall]Firewall; ConfigurationName=Sample_ArchiveFirewall;
                             InDesiredState=False}}
NumberOfResources          : 2
Type                       : Consistency
HostName                   : CONTOSO-PULLCLI
ResourcesInDesiredState    : {@{SourceInfo=C:\ReportTest\Sample_xFirewall_AddFirewallRule.ps1::16::9::Archive; ModuleName=PSDesiredStateConfiguration;
                             DurationInSeconds=2.672; InstanceName=ArchiveExample; StartDate=2016-04-04T11:21:55.7200000-07:00; ResourceName=Archive;
                             ModuleVersion=1.1; RebootRequested=False; ResourceId=[Archive]ArchiveExample; ConfigurationName=Sample_ArchiveFirewall;
                             InDesiredState=True}}
MACAddresses               : {00-1D-D8-B8-06-5C, 00-00-00-00-00-00-00-E0}
MetaConfiguration          : @{AgentId=52DA826D-00DE-4166-8ACB-73F2B46A7E00; ConfigurationDownloadManagers=System.Object[];
                             ActionAfterReboot=ContinueConfiguration; LCMCompatibleVersions=System.Object[]; LCMState=Idle;
                             ResourceModuleManagers=System.Object[]; ReportManagers=System.Object[]; StatusRetentionTimeInDays=10; LCMVersion=2.0;
                             ConfigurationMode=ApplyAndMonitor; RefreshFrequencyMins=30; RebootNodeIfNeeded=True; RefreshMode=Pull;
                             DebugMode=System.Object[]; LCMStateDetail=; AllowModuleOverwrite=False; ConfigurationModeFrequencyMins=15}
Locale                     : en-US
Mode                       : Pull
```

<span data-ttu-id="1f289-136">Mimo jiné to ukazuje, že volá nejaktuálnější konfiguraci dvou zdrojů a jeden z nich byl v požadovaném stavu a jeden z nich nebyl.</span><span class="sxs-lookup"><span data-stu-id="1f289-136">Among other things, this shows that the most recent configuration called two resources, and that one of them was in the desired state, and one of them was not.</span></span> <span data-ttu-id="1f289-137">Můžete získat pouze lépe čitelný výstup **ResourcesNotInDesiredState** vlastnost:</span><span class="sxs-lookup"><span data-stu-id="1f289-137">You can get a more readable output of just the **ResourcesNotInDesiredState** property:</span></span>

```powershell
$statusData.ResourcesInDesiredState
```

```output
SourceInfo        : C:\ReportTest\Sample_xFirewall_AddFirewallRule.ps1::16::9::Archive
ModuleName        : PSDesiredStateConfiguration
DurationInSeconds : 2.672
InstanceName      : ArchiveExample
StartDate         : 2016-04-04T11:21:55.7200000-07:00
ResourceName      : Archive
ModuleVersion     : 1.1
RebootRequested   : False
ResourceId        : [Archive]ArchiveExample
ConfigurationName : Sample_ArchiveFirewall
InDesiredState    : True
```

<span data-ttu-id="1f289-138">Všimněte si, že tyto příklady jsou určeny pro získáte představu, co můžete dělat s daty sestavy.</span><span class="sxs-lookup"><span data-stu-id="1f289-138">Note that these examples are meant to give you an idea of what you can do with report data.</span></span> <span data-ttu-id="1f289-139">Úvodní informace o práci s JSON v prostředí PowerShell najdete v tématu [přehrávání s JSON a PowerShell](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).</span><span class="sxs-lookup"><span data-stu-id="1f289-139">For an introduction on working with JSON in PowerShell, see [Playing with JSON and PowerShell](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).</span></span>

## <a name="see-also"></a><span data-ttu-id="1f289-140">Viz také</span><span class="sxs-lookup"><span data-stu-id="1f289-140">See Also</span></span>

[<span data-ttu-id="1f289-141">Konfigurace Local Configuration Manageru</span><span class="sxs-lookup"><span data-stu-id="1f289-141">Configuring the Local Configuration Manager</span></span>](../managing-nodes/metaConfig.md)

[<span data-ttu-id="1f289-142">Nastavení webového serveru vyžádané replikace DSC</span><span class="sxs-lookup"><span data-stu-id="1f289-142">Setting up a DSC web pull server</span></span>](pullServer.md)

[<span data-ttu-id="1f289-143">Použití konfiguračních názvů k nastavení načítacího klienta</span><span class="sxs-lookup"><span data-stu-id="1f289-143">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)