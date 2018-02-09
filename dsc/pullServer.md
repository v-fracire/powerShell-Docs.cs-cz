---
ms.date: 2018-02-02
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Vyžádání DSC služby"
ms.openlocfilehash: d5e24dcc093c73d8ebbaa618517193dacc4f2aaf
ms.sourcegitcommit: 755d7bc0740573d73613cedcf79981ca3dc81c5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/09/2018
---
# <a name="desired-state-configuration-pull-service"></a><span data-ttu-id="bad6a-103">Vyžádání služba Konfigurace požadovaného stavu</span><span class="sxs-lookup"><span data-stu-id="bad6a-103">Desired State Configuration Pull Service</span></span>

> <span data-ttu-id="bad6a-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="bad6a-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="bad6a-105">Správce místní konfigurace můžou být centrálně spravované řešením pro vyžádání obsahu služby.</span><span class="sxs-lookup"><span data-stu-id="bad6a-105">Local Configuration Manager can be centrally managed by a Pull Service solution.</span></span>
<span data-ttu-id="bad6a-106">Pokud používáte tuto metodu, je uzlu, který je spravován zaregistrován službou a přiřazen konfiguraci v LCM nastavení.</span><span class="sxs-lookup"><span data-stu-id="bad6a-106">When using this approach, the node that is being managed is registered with a service and assigned a configuration in LCM settings.</span></span>
<span data-ttu-id="bad6a-107">Konfigurace a všechny prostředky DSC potřebné jako závislosti pro konfiguraci se stáhnout do počítače a používá LCM ke správě konfigurace.</span><span class="sxs-lookup"><span data-stu-id="bad6a-107">The configuration and all DSC resources needed as dependencies for the configuration are downloaded to the machine and used by LCM to manage the configuration.</span></span>
<span data-ttu-id="bad6a-108">Informace o stavu je počítač spravován se odešlou do služby pro vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="bad6a-108">Information about the state of the machine being managed is uploaded to the service for reporting.</span></span>
<span data-ttu-id="bad6a-109">Tento koncept se označuje jako "vyžádání služba".</span><span class="sxs-lookup"><span data-stu-id="bad6a-109">This concept is referred to as "pull service".</span></span>

<span data-ttu-id="bad6a-110">Aktuální možnosti pro vyžádání obsahu službu:</span><span class="sxs-lookup"><span data-stu-id="bad6a-110">The current options for pull service include:</span></span>

- <span data-ttu-id="bad6a-111">Služba konfigurace stavu žádaný automatizace Azure</span><span class="sxs-lookup"><span data-stu-id="bad6a-111">Azure Automation Desired State Configuration service</span></span>
- <span data-ttu-id="bad6a-112">Vyžádání služby spuštěné v systému Windows Server</span><span class="sxs-lookup"><span data-stu-id="bad6a-112">A pull service running on Windows Server</span></span>
- <span data-ttu-id="bad6a-113">Komunita Udržovat řešení s otevřeným zdrojem</span><span class="sxs-lookup"><span data-stu-id="bad6a-113">Community maintained open source solutions</span></span>
- <span data-ttu-id="bad6a-114">Sdílené složce SMB</span><span class="sxs-lookup"><span data-stu-id="bad6a-114">An SMB share</span></span>

<span data-ttu-id="bad6a-115">**Doporučené řešení**, a s nejvíce funkcemi, které jsou k dispozici, není [Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-getting-started).</span><span class="sxs-lookup"><span data-stu-id="bad6a-115">**The recommended solution**, and the option with the most features available, is [Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-getting-started).</span></span>

<span data-ttu-id="bad6a-116">Uzly na místě v datových centrech privátní nebo veřejné cloudy, například Azure a AWS můžete spravovat službu Azure.</span><span class="sxs-lookup"><span data-stu-id="bad6a-116">The Azure service can manage nodes on-premises in private datacenters, or in public clouds such as Azure and AWS.</span></span>
<span data-ttu-id="bad6a-117">U privátních prostředí, kde nelze servery připojit přímo k Internetu, zvažte omezení odchozí provoz jenom publikované Azure rozsah IP adres (viz [rozsahy IP Datacentra Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span><span class="sxs-lookup"><span data-stu-id="bad6a-117">For private environments where servers cannot directly connect to the Internet, consider limiting outbound traffic to only the published Azure IP range (see [Azure Datacenter IP Ranges](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span></span>

<span data-ttu-id="bad6a-118">Funkce služby online, které nejsou momentálně k dispozici ve službě vyžádání v systému Windows Server:</span><span class="sxs-lookup"><span data-stu-id="bad6a-118">Features of the online service that are not currently available in the pull service on Windows Server include:</span></span>
- <span data-ttu-id="bad6a-119">Všechna data se šifrují během přenosu a v klidovém stavu</span><span class="sxs-lookup"><span data-stu-id="bad6a-119">All data is encrypted in transit and at rest</span></span>
- <span data-ttu-id="bad6a-120">Klientské certifikáty se vytváří a spravují automaticky</span><span class="sxs-lookup"><span data-stu-id="bad6a-120">Client certificates are created and managed automatically</span></span>
- <span data-ttu-id="bad6a-121">Ukládat tajné klíče pro centrální správu [hesla nebo přihlašovací údaje](https://docs.microsoft.com/en-us/azure/automation/automation-credentials), nebo [proměnné](https://docs.microsoft.com/en-us/azure/automation/automation-variables) například názvy serverů nebo připojovací řetězce</span><span class="sxs-lookup"><span data-stu-id="bad6a-121">Secrets store for centrally managing [passwords/credentials](https://docs.microsoft.com/en-us/azure/automation/automation-credentials), or [variables](https://docs.microsoft.com/en-us/azure/automation/automation-variables) such as server names or connection strings</span></span>
- <span data-ttu-id="bad6a-122">Centrálně spravovat uzlu [LCM konfigurace](metaConfig.md#basic-settings)</span><span class="sxs-lookup"><span data-stu-id="bad6a-122">Centrally manage node [LCM configuration](metaConfig.md#basic-settings)</span></span>
- <span data-ttu-id="bad6a-123">Centrálně přiřadit konfigurace pro klienta uzly</span><span class="sxs-lookup"><span data-stu-id="bad6a-123">Centrally assign configurations to client nodes</span></span>
- <span data-ttu-id="bad6a-124">Konfigurace verze se změní na "lesknice skupiny" pro testování dříve, než dorazila produkční</span><span class="sxs-lookup"><span data-stu-id="bad6a-124">Release configuration changes to "canary groups" for testing before reaching production</span></span>
- <span data-ttu-id="bad6a-125">Grafické vytváření sestav</span><span class="sxs-lookup"><span data-stu-id="bad6a-125">Graphical reporting</span></span>
  - <span data-ttu-id="bad6a-126">Podrobná sestava stavu na úrovni prostředků DSC členitosti</span><span class="sxs-lookup"><span data-stu-id="bad6a-126">Status detail at the DSC resource level of granularity</span></span>
  - <span data-ttu-id="bad6a-127">Podrobné chybové zprávy z klientských počítačů pro řešení potíží</span><span class="sxs-lookup"><span data-stu-id="bad6a-127">Verbose error messages from client machines for troubleshooting</span></span>
- <span data-ttu-id="bad6a-128">[Integrace s Azure Log Analytics](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-diagnostics) pro výstrahy, automatizované úlohy, aplikace pro Android nebo iOS pro vytváření sestav a výstrahy</span><span class="sxs-lookup"><span data-stu-id="bad6a-128">[Integration with Azure Log Analytics](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-diagnostics) for alerting, automated tasks, Android/iOS app for reporting and alerting</span></span>

## <a name="dsc-pull-service-in-windows-server"></a><span data-ttu-id="bad6a-129">DSC vyžádání služby v systému Windows Server</span><span class="sxs-lookup"><span data-stu-id="bad6a-129">DSC pull service in Windows Server</span></span>

<span data-ttu-id="bad6a-130">Je možné ke konfiguraci služby přijetí změn pro spouštění v systému Windows Server.</span><span class="sxs-lookup"><span data-stu-id="bad6a-130">It is possible to configuring a pull service to run on Windows Server.</span></span>
<span data-ttu-id="bad6a-131">Mějte na paměti, že řešení služby vyžádání obsahu, který je součástí systému Windows Server obsahuje pouze možnosti ukládání konfigurace nebo moduly pro stahování a zaznamenávání dat sestav v databázi.</span><span class="sxs-lookup"><span data-stu-id="bad6a-131">Please be advised that the pull service solution included in Windows Server includes only capabilities of storing configurations/modules for download and capturing report data in to database.</span></span>
<span data-ttu-id="bad6a-132">Nezahrnuje řadu funkce nabízené služby v Azure a proto není funkční nástroj pro vyhodnocení, jak se použije službu.</span><span class="sxs-lookup"><span data-stu-id="bad6a-132">It does not include many of the capabilities offered by the service in Azure and so is not a good tool for evaluating how the service would be used.</span></span>

<span data-ttu-id="bad6a-133">Službu vyžádání obsahu k dispozici v systému Windows Server je webová služba ve službě IIS, který používá rozhraní OData k dispozici DSC konfigurační soubory do cílové uzly uzly, zeptejte se pro ně.</span><span class="sxs-lookup"><span data-stu-id="bad6a-133">The pull service offered in Windows Server is a web service in IIS that uses an OData interface to make DSC configuration files available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="bad6a-134">Požadavky pro používání serveru vyžádané replikace:</span><span class="sxs-lookup"><span data-stu-id="bad6a-134">Requirements for using a pull server:</span></span>

- <span data-ttu-id="bad6a-135">Serveru se systémem:</span><span class="sxs-lookup"><span data-stu-id="bad6a-135">A server running:</span></span>
  - <span data-ttu-id="bad6a-136">WMF nebo PowerShell 5.0 nebo novější</span><span class="sxs-lookup"><span data-stu-id="bad6a-136">WMF/PowerShell 5.0 or greater</span></span>
  - <span data-ttu-id="bad6a-137">Role serveru IIS</span><span class="sxs-lookup"><span data-stu-id="bad6a-137">IIS server role</span></span>
  - <span data-ttu-id="bad6a-138">DSC služby</span><span class="sxs-lookup"><span data-stu-id="bad6a-138">DSC Service</span></span>
- <span data-ttu-id="bad6a-139">V ideálním případě některé znamená generování certifikát, k zabezpečení přihlašovacích údajů předaných na místní Configuration Manager (LCM) na cílové uzly</span><span class="sxs-lookup"><span data-stu-id="bad6a-139">Ideally, some means of generating a certificate, to secure credentials passed to the Local Configuration Manager (LCM) on target nodes</span></span>

<span data-ttu-id="bad6a-140">Nejlepší způsob, jak konfigurovat Windows Server k hostitelské službě. vyžádanou je použití konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="bad6a-140">The best way to configure Windows Server to host pull service is to use a DSC configuration.</span></span>
<span data-ttu-id="bad6a-141">Ukázkový skript je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="bad6a-141">An example script is provided below.</span></span>

### <a name="using-the-xdscwebservice-resource"></a><span data-ttu-id="bad6a-142">Pomocí xDSCWebService prostředků</span><span class="sxs-lookup"><span data-stu-id="bad6a-142">Using the xDSCWebService resource</span></span>

<span data-ttu-id="bad6a-143">Nejjednodušší způsob, jak nastavit webový server vyžádané replikace se má používat k prostředku xWebService, který je součástí modulu xPSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="bad6a-143">The easiest way to set up a web pull server is to use the xWebService resource, included in the xPSDesiredStateConfiguration module.</span></span>
<span data-ttu-id="bad6a-144">Následující kroky popisují, jak se daný prostředek v konfiguraci, která nastaví webovou službu.</span><span class="sxs-lookup"><span data-stu-id="bad6a-144">The following steps explain how to use the resource in a configuration that sets up the web service.</span></span>

1. <span data-ttu-id="bad6a-145">Volání [instalace modulu](https://technet.microsoft.com/en-us/library/dn807162.aspx) k instalaci **xPSDesiredStateConfiguration** modulu.</span><span class="sxs-lookup"><span data-stu-id="bad6a-145">Call the [Install-Module](https://technet.microsoft.com/en-us/library/dn807162.aspx) cmdlet to install the **xPSDesiredStateConfiguration** module.</span></span> <span data-ttu-id="bad6a-146">**Poznámka:**: **instalace modulu** je součástí **PowerShellGet** modul, který je součástí prostředí PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="bad6a-146">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="bad6a-147">Si můžete stáhnout **PowerShellGet** modul pro prostředí PowerShell 3.0 a 4.0 na [Preview moduly Powershellu PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="bad6a-147">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span> 
1. <span data-ttu-id="bad6a-148">Získání certifikátu SSL pro vyžádání obsahu DSC server od důvěryhodné certifikační autority, buď v rámci vaší organizace nebo z veřejné autority.</span><span class="sxs-lookup"><span data-stu-id="bad6a-148">Get an SSL certificate for the DSC Pull server from a trusted Certificate Authority, either within your organization or a public authority.</span></span> <span data-ttu-id="bad6a-149">Certifikát obdržený od autority je obvykle ve formátu PFX.</span><span class="sxs-lookup"><span data-stu-id="bad6a-149">The certificate received from the authority is usually in the PFX format.</span></span> <span data-ttu-id="bad6a-150">Nainstalujte certifikát na uzlu, který se stane DSC vyžádání serveru ve výchozím umístění, které by se měly CERT: \LocalMachine\My.</span><span class="sxs-lookup"><span data-stu-id="bad6a-150">Install the certificate on the node that will become the DSC Pull server in the default location which should be CERT:\LocalMachine\My.</span></span> <span data-ttu-id="bad6a-151">Poznamenejte si kryptografický otisk certifikátu.</span><span class="sxs-lookup"><span data-stu-id="bad6a-151">Make a note of the certificate thumbprint.</span></span>
1. <span data-ttu-id="bad6a-152">Vyberte identifikátor GUID, který má být použit jako registrační klíč.</span><span class="sxs-lookup"><span data-stu-id="bad6a-152">Select a GUID to be used as the Registration Key.</span></span> <span data-ttu-id="bad6a-153">Generovat jednu pomocí prostředí PowerShell zadejte následující PS řádku a stiskněte klávesu enter: '``` [guid]::newGuid()```'nebo'```New-Guid```'.</span><span class="sxs-lookup"><span data-stu-id="bad6a-153">To generate one using PowerShell enter the following at the PS prompt and press enter: '``` [guid]::newGuid()```' or '```New-Guid```'.</span></span> <span data-ttu-id="bad6a-154">Tento klíč se použije klient uzly jako sdílený klíč k ověření během registrace.</span><span class="sxs-lookup"><span data-stu-id="bad6a-154">This key will be used by client nodes as a shared key to authenticate during registration.</span></span> <span data-ttu-id="bad6a-155">Další informace najdete v části registrační klíč níže.</span><span class="sxs-lookup"><span data-stu-id="bad6a-155">For more information see the Registration Key section below.</span></span>
1. <span data-ttu-id="bad6a-156">V integrovaném Skriptovacím prostředí PowerShell, spusťte (F5) následující konfigurační skript (zahrnutý ve složce příklad **xPSDesiredStateConfiguration** modulu jako Sample_xDscWebService.ps1).</span><span class="sxs-lookup"><span data-stu-id="bad6a-156">In the PowerShell ISE, start (F5) the following configuration script (included in the Example folder of the  **xPSDesiredStateConfiguration** module as Sample_xDscWebService.ps1).</span></span> <span data-ttu-id="bad6a-157">Tento skript nastaví server vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="bad6a-157">This script sets up the pull server.</span></span>

```powershell
    configuration Sample_xDscPullServer
    {
        param
        (
                [string[]]$NodeName = 'localhost',

                [ValidateNotNullOrEmpty()]
                [string] $certificateThumbPrint,

                [Parameter(Mandatory)]
                [ValidateNotNullOrEmpty()]
                [string] $RegistrationKey
         )

         Import-DSCResource -ModuleName xPSDesiredStateConfiguration
         Import-DSCResource –ModuleName PSDesiredStateConfiguration

         Node $NodeName
         {
             WindowsFeature DSCServiceFeature
             {
                 Ensure = 'Present'
                 Name   = 'DSC-Service'
             }

             xDscWebService PSDSCPullServer
             {
                 Ensure                   = 'Present'
                 EndpointName             = 'PSDSCPullServer'
                 Port                     = 8080
                 PhysicalPath             = "$env:SystemDrive\inetpub\PSDSCPullServer"
                 CertificateThumbPrint    = $certificateThumbPrint
                 ModulePath               = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
                 ConfigurationPath        = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
                 State                    = 'Started'
                 DependsOn                = '[WindowsFeature]DSCServiceFeature'
                 UseSecurityBestPractices = $false
             }

            File RegistrationKeyFile
            {
                Ensure          = 'Present'
                Type            = 'File'
                DestinationPath = "$env:ProgramFiles\WindowsPowerShell\DscService\RegistrationKeys.txt"
                Contents        = $RegistrationKey
            }
        }
    }

```

1. <span data-ttu-id="bad6a-158">Spustit v konfiguraci předávání kryptografický otisk certifikátu SSL, jako **certificateThumbPrint** parametr a identifikátor GUID registrační klíč jako **RegistrationKey** parametr:</span><span class="sxs-lookup"><span data-stu-id="bad6a-158">Run the configuration, passing the thumbprint of the SSL certificate as the **certificateThumbPrint** parameter and a GUID registration key as the **RegistrationKey** parameter:</span></span>

```powershell
    # To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store 
    # and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
    dir Cert:\LocalMachine\my

    # Then include this thumbprint when running the configuration
    Sample_xDSCPullServer -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

    # Run the compiled configuration to make the target node a DSC Pull Server
    Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose

```

#### <a name="registration-key"></a><span data-ttu-id="bad6a-159">Registrační klíč</span><span class="sxs-lookup"><span data-stu-id="bad6a-159">Registration Key</span></span>

<span data-ttu-id="bad6a-160">Povolit klientské uzly registraci se serverem a používají názvy konfigurace místo ID konfigurace, registrační klíč, který byl vytvořen výše konfigurace je uložen v souboru s názvem `RegistrationKeys.txt` v `C:\Program Files\WindowsPowerShell\DscService`.</span><span class="sxs-lookup"><span data-stu-id="bad6a-160">To allow client nodes to register with the server so that they can use configuration names instead of a configuration ID, a registration key which was created by the above configuration is saved in a file named `RegistrationKeys.txt` in `C:\Program Files\WindowsPowerShell\DscService`.</span></span> <span data-ttu-id="bad6a-161">Registrační klíč funguje jako sdílený tajný klíč používá při počáteční registraci klienta se serverem pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="bad6a-161">The registration key functions as a shared secret used during the initial registration by the client with the pull server.</span></span> <span data-ttu-id="bad6a-162">Klient vygeneruje certifikát podepsaný svým držitelem, který slouží k jednoznačné ověření na serveru vyžádané replikace po úspěšném dokončení registrace se.</span><span class="sxs-lookup"><span data-stu-id="bad6a-162">The client will generate a self-signed certificate which is used to uniquely authenticate to the pull server once registration is successfully completed.</span></span> <span data-ttu-id="bad6a-163">Kryptografický otisk tohoto certifikátu je uložený místně a přidružené k adrese URL serveru pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="bad6a-163">The thumbprint of this certificate is stored locally and associated with the URL of the pull server.</span></span>
> <span data-ttu-id="bad6a-164">**Poznámka:**: registrace klíče nejsou podporovány v prostředí PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="bad6a-164">**Note**: Registration keys are not supported in PowerShell 4.0.</span></span> 

<span data-ttu-id="bad6a-165">Chcete-li nakonfigurovat uzel k ověření serveru vyžádané replikace registrace klíč musí být v metakonfiguraci pro cílový uzel, který bude registrace k tomuto serveru pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="bad6a-165">In order to configure a node to authenticate with the pull server the registration key needs to be in the metaconfiguration for any target node that will be registering with this pull server.</span></span> <span data-ttu-id="bad6a-166">Všimněte si, že **RegistrationKey** v metakonfiguraci níže se odebere po úspěšně zaregistrovala cílový počítač, a hodnota '140a952b-b9d6-406b-b416-e0f759c9c0e4' se musí shodovat s hodnotou uloženou v RegistrationKeys.txt soubor na tomto serveru.</span><span class="sxs-lookup"><span data-stu-id="bad6a-166">Note that the **RegistrationKey** in the metaconfiguration below is removed after the target machine has successfully registered, and that the value '140a952b-b9d6-406b-b416-e0f759c9c0e4' must match the value stored in the RegistrationKeys.txt file on the pull server.</span></span> <span data-ttu-id="bad6a-167">Vždy zacházet s hodnotou klíče registrace bezpečně, protože vědomí umožňuje, aby všechny cílové počítače k registraci se serverem pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="bad6a-167">Always treat the registration key value securely, because knowing it allows any target machine to register with the pull server.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
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
            ServerURL          = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey    = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('ClientConfig')
        }

        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
        }
    }
}

PullClientConfigID -OutputPath c:\Configs\TargetNodes


```

> <span data-ttu-id="bad6a-168">**Poznámka:**: **ReportServerWeb** části umožňuje data k odeslání na server vyžádané replikace pro vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="bad6a-168">**Note**: The **ReportServerWeb** section allows reporting data to be sent to the pull server.</span></span>

<span data-ttu-id="bad6a-169">Nedostatek **ConfigurationID** vlastnost v souboru metakonfiguraci implicitně znamená serveru vyžádané replikace se nepodporuje verze V2 protokol server vyžádané replikace, a proto je požadována počáteční registrace.</span><span class="sxs-lookup"><span data-stu-id="bad6a-169">The lack of the **ConfigurationID** property in the metaconfiguration file implicitly means that pull server is supporting the V2 version of the pull server protocol so an initial registration is required.</span></span>
<span data-ttu-id="bad6a-170">Naopak přítomnosti **ConfigurationID** znamená, že se používá protokol server vyžádané replikace verze V1 a neexistuje žádné zpracování registrace.</span><span class="sxs-lookup"><span data-stu-id="bad6a-170">Conversely, the presence of a **ConfigurationID** means that the V1 version of the pull server protocol is used and there is no registration processing.</span></span>

><span data-ttu-id="bad6a-171">**Poznámka:**: V PUSH scénáři chyby existuje v aktuální uvolňování, díky které je potřeba definovat ConfigurationID vlastnost v souboru metakonfiguraci pro uzly, které nikdy zaregistrovali načítacího serveru.</span><span class="sxs-lookup"><span data-stu-id="bad6a-171">**Note**: In a PUSH scenario, a bug exists in the current relase that makes it necessary to define a ConfigurationID property in the metaconfiguration file for nodes that have never registered with a pull server.</span></span> <span data-ttu-id="bad6a-172">Tato akce vynutí protokol serveru vyžádané replikace V1 a vyhnout zprávy o selhání registrace.</span><span class="sxs-lookup"><span data-stu-id="bad6a-172">This will force the V1 Pull Server protocol and avoid registration failure messages.</span></span>

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="bad6a-173">Umístění konfigurace a prostředky</span><span class="sxs-lookup"><span data-stu-id="bad6a-173">Placing configurations and resources</span></span>

<span data-ttu-id="bad6a-174">Po vyžádání obsahu server dokončení instalačního programu, složky, které jsou definované **ConfigurationPath** a **ModulePath** vlastnosti v konfiguraci serveru vyžádané replikace jsou, kam umístíte modulů a konfigurací které budou k dispozici pro cílové uzly načítat.</span><span class="sxs-lookup"><span data-stu-id="bad6a-174">After the pull server setup completes, the folders defined by the **ConfigurationPath** and **ModulePath** properties in the pull server configuration are where you will place modules and configurations that will be available for target nodes to pull.</span></span>
<span data-ttu-id="bad6a-175">Tyto soubory musí být v konkrétním formátu v pořadí pro vyžádání obsahu server správně zpracovat.</span><span class="sxs-lookup"><span data-stu-id="bad6a-175">These files need to be in a specific format in order for the pull server to correctly process them.</span></span>

### <a name="dsc-resource-module-package-format"></a><span data-ttu-id="bad6a-176">Formát balíčku modulu prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="bad6a-176">DSC resource module package format</span></span>

<span data-ttu-id="bad6a-177">Každý modul prostředků musí být ZIP a s názvem podle vzoru následující `{Module Name}_{Module Version}.zip`.</span><span class="sxs-lookup"><span data-stu-id="bad6a-177">Each resource module needs to be zipped and named according the following pattern `{Module Name}_{Module Version}.zip`.</span></span>
<span data-ttu-id="bad6a-178">Například modul s názvem xWebAdminstration verzí modulu 3.1.2.0 by se jmenovala 'xWebAdministration_3.2.1.0.zip'.</span><span class="sxs-lookup"><span data-stu-id="bad6a-178">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named 'xWebAdministration_3.2.1.0.zip'.</span></span>
<span data-ttu-id="bad6a-179">Každá verze nástroje modul musí být obsažena v souboru zip jeden.</span><span class="sxs-lookup"><span data-stu-id="bad6a-179">Each version of a module must be contained in a single zip file.</span></span>
<span data-ttu-id="bad6a-180">Vzhledem k tomu, že existuje jenom jedna verze nástroje prostředků do každého souboru zip modulu formát přidali v WMF 5.0 s není dostupná podpora pro více verze modulu v jednom adresáři.</span><span class="sxs-lookup"><span data-stu-id="bad6a-180">Since there is only a single version of a resource in each zip file the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span>
<span data-ttu-id="bad6a-181">To znamená, že před zabalení moduly prostředků DSC pro použití s načítacího serveru budete muset provést změnu malá strukturu adresáře.</span><span class="sxs-lookup"><span data-stu-id="bad6a-181">This means that before packaging up DSC resource modules for use with pull server you will need to make a small change to the directory structure.</span></span>
<span data-ttu-id="bad6a-182">Výchozí formát modulů obsahující prostředek DSC v WMF 5.0 je ' {složku modulu}\{verze modulu} \DscResources\{Složka prostředků DSC}\'.</span><span class="sxs-lookup"><span data-stu-id="bad6a-182">The default format of modules containing DSC resource in WMF 5.0 is '{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\'.</span></span>
<span data-ttu-id="bad6a-183">Před balení pro vyžádání obsahu server jednoduše odeberte **{verze modulu}** složku, cesta k přestane ' {složku modulu} \DscResources\{Složka prostředků DSC}\'.</span><span class="sxs-lookup"><span data-stu-id="bad6a-183">Before packaging up for the pull server simply remove the **{Module version}** folder so the path becomes '{Module Folder}\DscResources\{DSC Resource Folder}\'.</span></span>
<span data-ttu-id="bad6a-184">Díky této změně zip složce, jak je popsáno výše a nastavovat tyto soubory zip v **ModulePath** složky.</span><span class="sxs-lookup"><span data-stu-id="bad6a-184">With this change, zip the folder as described above and place these zip files in the **ModulePath** folder.</span></span>

<span data-ttu-id="bad6a-185">Použití `new-dscchecksum {module zip file}` vytvořte soubor kontrolního součtu pro modul nově přidaná.</span><span class="sxs-lookup"><span data-stu-id="bad6a-185">Use `new-dscchecksum {module zip file}` to create a checksum file for the newly-added module.</span></span>

### <a name="configuration-mof-format"></a><span data-ttu-id="bad6a-186">Formát MOF konfigurace</span><span class="sxs-lookup"><span data-stu-id="bad6a-186">Configuration MOF format</span></span>

<span data-ttu-id="bad6a-187">Konfigurační soubor MOF musí být spárována s soubor kontrolního součtu, takže LCM na cílový uzel můžete konfiguraci ověřit.</span><span class="sxs-lookup"><span data-stu-id="bad6a-187">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span>
<span data-ttu-id="bad6a-188">Chcete-li vytvořit kontrolní součet, zavolejte [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="bad6a-188">To create a checksum, call the [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) cmdlet.</span></span>
<span data-ttu-id="bad6a-189">Rutina trvá **cesta** parametr, který určuje složku, kde se nachází v konfiguraci MOF.</span><span class="sxs-lookup"><span data-stu-id="bad6a-189">The cmdlet takes a **Path** parameter that specifies the folder where the configuration MOF is located.</span></span>
<span data-ttu-id="bad6a-190">Rutina vytvoří kontrolní součet souboru s názvem `ConfigurationMOFName.mof.checksum`, kde `ConfigurationMOFName` je název konfiguračního souboru mof.</span><span class="sxs-lookup"><span data-stu-id="bad6a-190">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span>
<span data-ttu-id="bad6a-191">Pokud existují minimálně jedna konfigurace soubory MOF do určené složky, vytvoří se pro každou konfiguraci ve složce kontrolní součet.</span><span class="sxs-lookup"><span data-stu-id="bad6a-191">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span>
<span data-ttu-id="bad6a-192">Umístěte soubory MOF a jejich přidružené kontrolního součtu souborů v **ConfigurationPath** složky.</span><span class="sxs-lookup"><span data-stu-id="bad6a-192">Place the MOF files and their associated checksum files in the **ConfigurationPath** folder.</span></span>

><span data-ttu-id="bad6a-193">**Poznámka:**: Pokud změníte konfigurační soubor MOF žádným způsobem, musíte také znovu vytvořit soubor kontrolního součtu.</span><span class="sxs-lookup"><span data-stu-id="bad6a-193">**Note**: If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

### <a name="tooling"></a><span data-ttu-id="bad6a-194">Nástrojů</span><span class="sxs-lookup"><span data-stu-id="bad6a-194">Tooling</span></span>

<span data-ttu-id="bad6a-195">Chcete-li nastavení tvoří, ověření a Správa serveru vyžádané replikace jednodušší, tyto nástroje jsou zahrnuty jako příklady v nejnovější verzi modulu xPSDesiredStateConfiguration:</span><span class="sxs-lookup"><span data-stu-id="bad6a-195">In order to make setting up, validating and managing the pull server easier, the following tools are included as examples in the latest version of the xPSDesiredStateConfiguration module:</span></span>

1. <span data-ttu-id="bad6a-196">Modul, který vám pomůže s balení moduly prostředků DSC a konfigurační soubory pro použití na tomto serveru.</span><span class="sxs-lookup"><span data-stu-id="bad6a-196">A module that will help with packaging DSC resource modules and configuration files for use on the pull server.</span></span> <span data-ttu-id="bad6a-197">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span><span class="sxs-lookup"><span data-stu-id="bad6a-197">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span></span> <span data-ttu-id="bad6a-198">Následující příklady:</span><span class="sxs-lookup"><span data-stu-id="bad6a-198">Examples below:</span></span>

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @("xWebAdministration", "xPhp") 
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList 

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. <span data-ttu-id="bad6a-199">Skript, který ověří načítacího serveru správně nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="bad6a-199">A script that validates the pull server is configured correctly.</span></span> <span data-ttu-id="bad6a-200">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span><span class="sxs-lookup"><span data-stu-id="bad6a-200">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span></span>

## <a name="community-solutions-for-pull-service"></a><span data-ttu-id="bad6a-201">Řešení komunity pro vyžádání obsahu služby</span><span class="sxs-lookup"><span data-stu-id="bad6a-201">Community Solutions for Pull Service</span></span>

<span data-ttu-id="bad6a-202">Komunita DSC má vytvořené více řešení k implementaci protokol služby vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="bad6a-202">The DSC community has authored multiple solutions to implement the pull service protocol.</span></span>
<span data-ttu-id="bad6a-203">Pro místní prostředí, které tyto nabízí možnosti služby vyžádání obsahu a možnost přispívat zpět do komunity Přírůstkové vylepšení.</span><span class="sxs-lookup"><span data-stu-id="bad6a-203">For on-premises environments these offer pull service capabilities and an opportunity to contribute back to the community with incremental enhancements.</span></span>

- [<span data-ttu-id="bad6a-204">Tug</span><span class="sxs-lookup"><span data-stu-id="bad6a-204">Tug</span></span>](https://github.com/powershellorg/tug)
- [<span data-ttu-id="bad6a-205">DSC-TRÆK</span><span class="sxs-lookup"><span data-stu-id="bad6a-205">DSC-TRÆK</span></span>](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a><span data-ttu-id="bad6a-206">Konfigurace klienta pro vyžádání obsahu</span><span class="sxs-lookup"><span data-stu-id="bad6a-206">Pull client configuration</span></span>

<span data-ttu-id="bad6a-207">Následující témata popisují nastavení klientů pro vyžádání obsahu podrobně:</span><span class="sxs-lookup"><span data-stu-id="bad6a-207">The following topics describe setting up pull clients in detail:</span></span>

- [<span data-ttu-id="bad6a-208">Nastavení klienta vyžádání DSC pomocí ID konfigurace</span><span class="sxs-lookup"><span data-stu-id="bad6a-208">Setting up a DSC pull client using a configuration ID</span></span>](pullClientConfigID.md)
- [<span data-ttu-id="bad6a-209">Nastavení klienta vyžádání DSC pomocí názvy konfigurace</span><span class="sxs-lookup"><span data-stu-id="bad6a-209">Setting up a DSC pull client using configuration names</span></span>](pullClientConfigNames.md)
- [<span data-ttu-id="bad6a-210">Částečné konfigurace</span><span class="sxs-lookup"><span data-stu-id="bad6a-210">Partial configurations</span></span>](partialConfigs.md)

## <a name="see-also"></a><span data-ttu-id="bad6a-211">Viz taky</span><span class="sxs-lookup"><span data-stu-id="bad6a-211">See also</span></span>

- [<span data-ttu-id="bad6a-212">Přehled stavu konfigurace požadovaného prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="bad6a-212">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
- [<span data-ttu-id="bad6a-213">Přijetí konfigurace</span><span class="sxs-lookup"><span data-stu-id="bad6a-213">Enacting configurations</span></span>](enactingConfigurations.md)
- [<span data-ttu-id="bad6a-214">Použití serveru sestav DSC</span><span class="sxs-lookup"><span data-stu-id="bad6a-214">Using a DSC report server</span></span>](reportServer.md)
