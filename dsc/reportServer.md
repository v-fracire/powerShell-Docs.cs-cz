---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Použití serveru sestav DSC
ms.openlocfilehash: e239414dc30c7458c509392792d4775d04f2311a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="using-a-dsc-report-server"></a><span data-ttu-id="17f23-103">Použití serveru sestav DSC</span><span class="sxs-lookup"><span data-stu-id="17f23-103">Using a DSC report server</span></span>

> <span data-ttu-id="17f23-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="17f23-104">Applies To: Windows PowerShell 5.0</span></span>

><span data-ttu-id="17f23-105">**Poznámka:** serveru sestav, které jsou popsané v tomto tématu není k dispozici v prostředí PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="17f23-105">**Note:** The report server described in this topic is not available in PowerShell 4.0.</span></span>

<span data-ttu-id="17f23-106">Pokud chcete zasílat zprávy o jeho konfiguraci stavu na vyžádání obsahu server, který může být dotazován načíst data lze nakonfigurovat místní Configuration Manager (LCM) uzlu.</span><span class="sxs-lookup"><span data-stu-id="17f23-106">The Local Configuration Manager (LCM) of a node can be configured to send reports about its configuration status to a pull server, which can then be queried to retrieve that data.</span></span> <span data-ttu-id="17f23-107">Pokaždé, když uzel ověří a použije konfiguraci, odešle sestavy na server sestav.</span><span class="sxs-lookup"><span data-stu-id="17f23-107">Each time the node checks and applies a configuration, it sends a report to the report server.</span></span> <span data-ttu-id="17f23-108">Tyto sestavy jsou uloženy v databázi na serveru a může načíst volání webové služby generování sestav.</span><span class="sxs-lookup"><span data-stu-id="17f23-108">These reports are stored in a database on the server, and can be retrieved by calling the reporting web service.</span></span> <span data-ttu-id="17f23-109">Každá sestava obsahuje informace, například jaký konfigurace byly použity, a jestli se úspěšně, používá prostředky, všechny chyby, které byly vyvolány a zahájení a dokončení časy.</span><span class="sxs-lookup"><span data-stu-id="17f23-109">Each report contains information such as what configurations were applied and whether they succeeded, the resources used, any errors that were thrown, and start and finish times.</span></span>

## <a name="configuring-a-node-to-send-reports"></a><span data-ttu-id="17f23-110">Konfigurace uzlu, pokud chcete zasílat zprávy</span><span class="sxs-lookup"><span data-stu-id="17f23-110">Configuring a node to send reports</span></span>

<span data-ttu-id="17f23-111">Zjistit uzel pro odesílají sestavy na server pomocí **ReportServerWeb** blokovat v konfiguraci uzlu LCM (informace o konfiguraci LCM najdete v tématu [konfigurace správce místní konfigurace](metaConfig.md) ).</span><span class="sxs-lookup"><span data-stu-id="17f23-111">You tell a node to send reports to a server by using a **ReportServerWeb** block in the node's LCM configuration (for information about configuring the LCM, see [Configuring the Local Configuration Manager](metaConfig.md)).</span></span> <span data-ttu-id="17f23-112">Server, na kterou uzlu, odešle sestavy musí nastavit jako vyžadování webový server (sestavy nelze odeslat ke sdílené složce protokolu SMB).</span><span class="sxs-lookup"><span data-stu-id="17f23-112">The server to which the node sends reports must be set up as a web pull server (you cannot send reports to an SMB share).</span></span> <span data-ttu-id="17f23-113">Informace o nastavení serveru vyžádané replikace najdete v tématu [nastavení webového serveru vyžádané replikace DSC](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="17f23-113">For information about setting up a pull server, see [Setting up a DSC web pull server](pullServer.md).</span></span> <span data-ttu-id="17f23-114">Server sestav může být stejnou službu, ze kterého uzlu vrátí konfigurace a získá prostředky, nebo může být jinou službu.</span><span class="sxs-lookup"><span data-stu-id="17f23-114">The report server can be the same service from which the node pulls configurations and gets resources, or it can be a different service.</span></span>

<span data-ttu-id="17f23-115">V **ReportServerWeb** bloku, zadejte adresu URL služby vyžádání obsahu a registrační klíč, který se označuje k serveru.</span><span class="sxs-lookup"><span data-stu-id="17f23-115">In the **ReportServerWeb** block, you specify the URL of the pull service and a registration key that is known to the server.</span></span>

<span data-ttu-id="17f23-116">Následující konfigurace nakonfiguruje uzel pro vyžádání obsahu konfigurace z jedné služby a služby na jiném serveru, odesílat sestavy.</span><span class="sxs-lookup"><span data-stu-id="17f23-116">The following configuration configures a node to pull configurations from one service, and send reports to a service on a different server.</span></span>

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

<span data-ttu-id="17f23-117">Nakonfiguruje následující konfigurace uzlu používat jeden server pro konfigurace, prostředky a vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="17f23-117">The following configuration configures a node to use a single server for configurations, resources, and reporting.</span></span>

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

><span data-ttu-id="17f23-118">**Poznámka:** můžete pojmenovat webovou službu všechno při nastavení na server vyžádané replikace, ale **ServerURL** vlastnost musí odpovídat názvu služby.</span><span class="sxs-lookup"><span data-stu-id="17f23-118">**Note:** You can name the web service whatever you want when you set up a pull server, but the **ServerURL** property must match the service name.</span></span>

## <a name="getting-report-data"></a><span data-ttu-id="17f23-119">Získávání dat sestavy</span><span class="sxs-lookup"><span data-stu-id="17f23-119">Getting report data</span></span>

<span data-ttu-id="17f23-120">Sestavy odeslat na server vyžádané replikace jsou vloženy do databáze na serveru.</span><span class="sxs-lookup"><span data-stu-id="17f23-120">Reports sent to the pull server are entered into a database on the server.</span></span> <span data-ttu-id="17f23-121">Sestavy jsou k dispozici prostřednictvím volání webové služby.</span><span class="sxs-lookup"><span data-stu-id="17f23-121">The reports are available through calls to the web service.</span></span> <span data-ttu-id="17f23-122">K načtení sestavy pro konkrétním uzlu, odeslání požadavku HTTP k webové službě sestavy v následující podobě: `http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId= 'MyNodeAgentId')/Reports` kde `MyNodeAgentId` je ID agenta uzlu, pro kterou chcete získat sestavy.</span><span class="sxs-lookup"><span data-stu-id="17f23-122">To retrieve reports for a specific node, send an HTTP request to the report web service in the following form: `http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId= 'MyNodeAgentId')/Reports` where `MyNodeAgentId` is the AgentId of the node for which you want to get reports.</span></span> <span data-ttu-id="17f23-123">Můžete získat ID agenta pro uzel voláním [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx) v tomto uzlu.</span><span class="sxs-lookup"><span data-stu-id="17f23-123">You can get the AgentID for a node by calling [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx) on that node.</span></span>

<span data-ttu-id="17f23-124">Sestavy se vrátí jako pole objektů JSON.</span><span class="sxs-lookup"><span data-stu-id="17f23-124">The reports are returned as an array of JSON objects.</span></span>

<span data-ttu-id="17f23-125">Následující skript vrátí sestavy pro uzel, na kterém je spuštěna:</span><span class="sxs-lookup"><span data-stu-id="17f23-125">The following script returns the reports for the node on which it is run:</span></span>

```powershell
function GetReport
{
    param($AgentId = "$((glcm).AgentId)", $serviceURL = "http://CONTOSO-REPORT:8080/PSDSCPullServer.svc")
    $requestUri = "$serviceURL/Nodes(AgentId= '$AgentId')/Reports"
    $request = Invoke-WebRequest -Uri $requestUri  -ContentType "application/json;odata=minimalmetadata;streaming=true;charset=utf-8" `
               -UseBasicParsing -Headers @{Accept = "application/json";ProtocolVersion = "2.0"} `
               -ErrorAction SilentlyContinue -ErrorVariable ev
    $object = ConvertFrom-Json $request.content
    return $object.value
}
```

## <a name="viewing-report-data"></a><span data-ttu-id="17f23-126">Zobrazení dat sestavy</span><span class="sxs-lookup"><span data-stu-id="17f23-126">Viewing report data</span></span>

<span data-ttu-id="17f23-127">Pokud nastavíte proměnnou na výsledek **GetReport** funkce, můžete zobrazit jednotlivých polí v elementu pole, která je vrácena:</span><span class="sxs-lookup"><span data-stu-id="17f23-127">If you set a variable to the result of the **GetReport** function, you can view the individual fields in an element of the array that is returned:</span></span>

```powershell
$reports = GetReport
$reports[1]


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

<span data-ttu-id="17f23-128">Ve výchozím nastavení, sestavy jsou seřazené podle **JobID**.</span><span class="sxs-lookup"><span data-stu-id="17f23-128">By default, the reports are sorted by **JobID**.</span></span> <span data-ttu-id="17f23-129">Chcete-li získat nejnovější sestavu, můžete sestavy seřadit podle sestupném **StartTime** vlastnost a potom get první prvek pole:</span><span class="sxs-lookup"><span data-stu-id="17f23-129">To get the most recent report, you can sort the reports by descending **StartTime** property, and then get the first element of the array:</span></span>

```powershell
$reportsByStartTime = $reports | Sort-Object {$_."StartTime" -as [DateTime] } -Descending
$reportMostRecent = $reportsByStartTime[0]
```

<span data-ttu-id="17f23-130">Všimněte si, že **StatusData** vlastnost je objekt s číslem vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="17f23-130">Notice that the **StatusData** property is an object with a number of properties.</span></span> <span data-ttu-id="17f23-131">Toto je, kde je mnohem data pro generování sestav.</span><span class="sxs-lookup"><span data-stu-id="17f23-131">This is where much of the reporting data is.</span></span> <span data-ttu-id="17f23-132">Podívejme se na jednotlivé pole **StatusData** vlastnost na nejnovější sestavu:</span><span class="sxs-lookup"><span data-stu-id="17f23-132">Let's look at the individual fields of the **StatusData** property for the most recent report:</span></span>

```powershell
$statusData = $reportMostRecent.StatusData | ConvertFrom-Json
$statusData

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

<span data-ttu-id="17f23-133">To mimo jiné to ukazuje, že nejaktuálnější konfiguraci názvem dva prostředky a jeden z nich byla v požadovaném stavu a jeden z nich nebyl.</span><span class="sxs-lookup"><span data-stu-id="17f23-133">Among other things, this shows that the most recent configuration called two resources, and that one of them was in the desired state, and one of them was not.</span></span> <span data-ttu-id="17f23-134">Můžete získat jen na čtení výstup **ResourcesNotInDesiredState** vlastnost:</span><span class="sxs-lookup"><span data-stu-id="17f23-134">You can get a more readable output of just the **ResourcesNotInDesiredState** property:</span></span>

```powershell
$statusData.ResourcesInDesiredState

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

<span data-ttu-id="17f23-135">Všimněte si, že tyto příklady jsou určené získáte představu o co můžete dělat s daty sestavy.</span><span class="sxs-lookup"><span data-stu-id="17f23-135">Note that these examples are meant to give you an idea of what you can do with report data.</span></span> <span data-ttu-id="17f23-136">Úvodní informace o práci s JSON v prostředí PowerShell, naleznete [přehrávání s protokoly JSON a prostředí PowerShell](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).</span><span class="sxs-lookup"><span data-stu-id="17f23-136">For an introduction on working with JSON in PowerShell, see [Playing with JSON and PowerShell](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).</span></span>

## <a name="see-also"></a><span data-ttu-id="17f23-137">Viz také</span><span class="sxs-lookup"><span data-stu-id="17f23-137">See Also</span></span>
- [<span data-ttu-id="17f23-138">Konfigurace správce místní konfigurace</span><span class="sxs-lookup"><span data-stu-id="17f23-138">Configuring the Local Configuration Manager</span></span>](metaConfig.md)
- [<span data-ttu-id="17f23-139">Nastavení webového serveru vyžádané replikace DSC</span><span class="sxs-lookup"><span data-stu-id="17f23-139">Setting up a DSC web pull server</span></span>](pullServer.md)
- [<span data-ttu-id="17f23-140">Použití konfiguračních názvů k nastavení načítacího klienta</span><span class="sxs-lookup"><span data-stu-id="17f23-140">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)