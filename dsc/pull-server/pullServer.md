---
ms.date: 04/11/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Načítací služba DSC
ms.openlocfilehash: 659a8f8b2ce7d34058e789c5de336dc1f1f2abb2
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403739"
---
# <a name="desired-state-configuration-pull-service"></a><span data-ttu-id="943c3-103">Načítací služba Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="943c3-103">Desired State Configuration Pull Service</span></span>

> <span data-ttu-id="943c3-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="943c3-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="943c3-105">Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="943c3-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="943c3-106">Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="943c3-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="943c3-107">Local Configuration Manageru můžete centrálně spravovat řešení o přijetí změn služby.</span><span class="sxs-lookup"><span data-stu-id="943c3-107">Local Configuration Manager can be centrally managed by a Pull Service solution.</span></span>
<span data-ttu-id="943c3-108">Při použití tohoto přístupu je uzel, který je spravován registrován pomocí služby a přiřazené konfigurace LCM nastavení.</span><span class="sxs-lookup"><span data-stu-id="943c3-108">When using this approach, the node that is being managed is registered with a service and assigned a configuration in LCM settings.</span></span>
<span data-ttu-id="943c3-109">Konfigurace a všechny prostředky DSC potřebné jako závislosti pro konfiguraci se stáhl do počítače a slouží ke správě konfigurace LCM.</span><span class="sxs-lookup"><span data-stu-id="943c3-109">The configuration and all DSC resources needed as dependencies for the configuration are downloaded to the machine and used by LCM to manage the configuration.</span></span>
<span data-ttu-id="943c3-110">Informace o stavu je počítač spravován se odešlou do služby pro vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="943c3-110">Information about the state of the machine being managed is uploaded to the service for reporting.</span></span>
<span data-ttu-id="943c3-111">Tento koncept se označuje jako "službu přijetí změn."</span><span class="sxs-lookup"><span data-stu-id="943c3-111">This concept is referred to as "pull service."</span></span>

<span data-ttu-id="943c3-112">Aktuální možnosti pro službu přijetí změn:</span><span class="sxs-lookup"><span data-stu-id="943c3-112">The current options for pull service include:</span></span>

- <span data-ttu-id="943c3-113">Služba Azure Automation Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="943c3-113">Azure Automation Desired State Configuration service</span></span>
- <span data-ttu-id="943c3-114">Načítací služba běží na Windows serveru</span><span class="sxs-lookup"><span data-stu-id="943c3-114">A pull service running on Windows Server</span></span>
- <span data-ttu-id="943c3-115">Udržuje komunity open source řešení</span><span class="sxs-lookup"><span data-stu-id="943c3-115">Community maintained open-source solutions</span></span>
- <span data-ttu-id="943c3-116">Do sdílené složky SMB</span><span class="sxs-lookup"><span data-stu-id="943c3-116">An SMB share</span></span>

<span data-ttu-id="943c3-117">**Doporučené řešení**, a možnost s nejvíce funkcemi, které jsou k dispozici, je [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span><span class="sxs-lookup"><span data-stu-id="943c3-117">**The recommended solution**, and the option with the most features available, is [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span></span>

<span data-ttu-id="943c3-118">Služba Azure můžete spravovat uzly s místními v privátní síti datových center nebo ve veřejných cloudech, jako jsou Azure a AWS.</span><span class="sxs-lookup"><span data-stu-id="943c3-118">The Azure service can manage nodes on-premises in private datacenters, or in public clouds such as Azure and AWS.</span></span>
<span data-ttu-id="943c3-119">Pro privátní prostředí, kde servery nemohou připojit přímo k Internetu, zvažte omezení odchozího provozu do publikované rozsah IP adres Azure (viz [Azure rozsahů IP adres Datacentra](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span><span class="sxs-lookup"><span data-stu-id="943c3-119">For private environments where servers cannot directly connect to the Internet, consider limiting outbound traffic to only the published Azure IP range (see [Azure Datacenter IP Ranges](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span></span>

<span data-ttu-id="943c3-120">Funkce služby online, které nejsou aktuálně dostupné ve službě o přijetí změn ve Windows serveru:</span><span class="sxs-lookup"><span data-stu-id="943c3-120">Features of the online service that are not currently available in the pull service on Windows Server include:</span></span>
- <span data-ttu-id="943c3-121">Všechna data se šifrují přenášená i neaktivní</span><span class="sxs-lookup"><span data-stu-id="943c3-121">All data is encrypted in transit and at rest</span></span>
- <span data-ttu-id="943c3-122">Vytvoření a správa automaticky klientské certifikáty</span><span class="sxs-lookup"><span data-stu-id="943c3-122">Client certificates are created and managed automatically</span></span>
- <span data-ttu-id="943c3-123">Uložení tajných kódů pro centrální správu [hesla nebo přihlašovací údaje](/azure/automation/automation-credentials), nebo [proměnné](/azure/automation/automation-variables) například názvy serverů nebo připojovací řetězce</span><span class="sxs-lookup"><span data-stu-id="943c3-123">Secrets store for centrally managing [passwords/credentials](/azure/automation/automation-credentials), or [variables](/azure/automation/automation-variables) such as server names or connection strings</span></span>
- <span data-ttu-id="943c3-124">Centrálně spravovat uzel [konfigurace LCM](../managing-nodes/metaConfig.md#basic-settings)</span><span class="sxs-lookup"><span data-stu-id="943c3-124">Centrally manage node [LCM configuration](../managing-nodes/metaConfig.md#basic-settings)</span></span>
- <span data-ttu-id="943c3-125">Centrálně přiřadit konfigurace k uzlům klienta</span><span class="sxs-lookup"><span data-stu-id="943c3-125">Centrally assign configurations to client nodes</span></span>
- <span data-ttu-id="943c3-126">Konfigurace vydané verze se změní na "testovací skupiny" pro testování před dosažením produkčního prostředí</span><span class="sxs-lookup"><span data-stu-id="943c3-126">Release configuration changes to "canary groups" for testing before reaching production</span></span>
- <span data-ttu-id="943c3-127">Grafické vytváření sestav</span><span class="sxs-lookup"><span data-stu-id="943c3-127">Graphical reporting</span></span>
  - <span data-ttu-id="943c3-128">Podrobnosti stavu na úrovni členitosti prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="943c3-128">Status detail at the DSC resource level of granularity</span></span>
  - <span data-ttu-id="943c3-129">Podrobné chybové zprávy z klientských počítačů pro řešení potíží</span><span class="sxs-lookup"><span data-stu-id="943c3-129">Verbose error messages from client machines for troubleshooting</span></span>
- <span data-ttu-id="943c3-130">[Integrace s Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) pro výstrahy, automatizovaných úloh, aplikace pro Android nebo iOS pro generování sestav a upozorňování</span><span class="sxs-lookup"><span data-stu-id="943c3-130">[Integration with Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) for alerting, automated tasks, Android/iOS app for reporting and alerting</span></span>

## <a name="dsc-pull-service-in-windows-server"></a><span data-ttu-id="943c3-131">Načítací služba DSC v systému Windows Server</span><span class="sxs-lookup"><span data-stu-id="943c3-131">DSC pull service in Windows Server</span></span>

<span data-ttu-id="943c3-132">Je možné ke konfiguraci službu o přijetí změn, která běží na Windows serveru.</span><span class="sxs-lookup"><span data-stu-id="943c3-132">It is possible to configuring a pull service to run on Windows Server.</span></span>
<span data-ttu-id="943c3-133">Informováni, že řešení služby o přijetí změn ve Windows serveru zahrnuje pouze možnosti ukládání konfigurace/moduly ke stažení a zaznamenávání dat sestavy do databáze.</span><span class="sxs-lookup"><span data-stu-id="943c3-133">Be advised that the pull service solution included in Windows Server includes only capabilities of storing configurations/modules for download and capturing report data in to database.</span></span>
<span data-ttu-id="943c3-134">Nezahrnuje mnoho funkcí, které nabízí služba v Azure a proto není nástroj vhodný pro vaše rozhodnutí vyzkoušet by použití služby.</span><span class="sxs-lookup"><span data-stu-id="943c3-134">It does not include many of the capabilities offered by the service in Azure and so is not a good tool for evaluating how the service would be used.</span></span>

<span data-ttu-id="943c3-135">Načítací služba nabízí ve Windows serveru je webová služba ve službě IIS, která používá rozhraní OData DSC konfigurační soubory k dispozici na na cílové uzly ty uzly, požádat o nich.</span><span class="sxs-lookup"><span data-stu-id="943c3-135">The pull service offered in Windows Server is a web service in IIS that uses an OData interface to make DSC configuration files available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="943c3-136">Požadavky na použití serveru vyžádané replikace:</span><span class="sxs-lookup"><span data-stu-id="943c3-136">Requirements for using a pull server:</span></span>

- <span data-ttu-id="943c3-137">Serveru se systémem:</span><span class="sxs-lookup"><span data-stu-id="943c3-137">A server running:</span></span>
  - <span data-ttu-id="943c3-138">WMF/PowerShell 5.0 nebo novější</span><span class="sxs-lookup"><span data-stu-id="943c3-138">WMF/PowerShell 5.0 or greater</span></span>
  - <span data-ttu-id="943c3-139">Role serveru služby IIS</span><span class="sxs-lookup"><span data-stu-id="943c3-139">IIS server role</span></span>
  - <span data-ttu-id="943c3-140">Služba DSC</span><span class="sxs-lookup"><span data-stu-id="943c3-140">DSC Service</span></span>
- <span data-ttu-id="943c3-141">V ideálním případě některé znamená, že generování certifikát k zabezpečení přihlašovacích údajů předaných do místní Configuration Manageru (LCM) na cílové uzly</span><span class="sxs-lookup"><span data-stu-id="943c3-141">Ideally, some means of generating a certificate, to secure credentials passed to the Local Configuration Manager (LCM) on target nodes</span></span>

<span data-ttu-id="943c3-142">Nejlepší způsob, jak konfigurovat Windows Server k hostitelské službě modulu o přijetí změn je chcete použít konfiguraci DSC.</span><span class="sxs-lookup"><span data-stu-id="943c3-142">The best way to configure Windows Server to host pull service is to use a DSC configuration.</span></span>
<span data-ttu-id="943c3-143">Ukázkový skript jsou uvedeny níže.</span><span class="sxs-lookup"><span data-stu-id="943c3-143">An example script is provided below.</span></span>

### <a name="supported-database-systems"></a><span data-ttu-id="943c3-144">Podporované databázové systémy</span><span class="sxs-lookup"><span data-stu-id="943c3-144">Supported database systems</span></span>

|<span data-ttu-id="943c3-145">WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="943c3-145">WMF 4.0</span></span>   |<span data-ttu-id="943c3-146">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="943c3-146">WMF 5.0</span></span>  |<span data-ttu-id="943c3-147">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="943c3-147">WMF 5.1</span></span> |<span data-ttu-id="943c3-148">WMF 5.1 (Windows Server Insider Preview 17090)</span><span class="sxs-lookup"><span data-stu-id="943c3-148">WMF 5.1 (Windows Server Insider Preview 17090)</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="943c3-149">MDB</span><span class="sxs-lookup"><span data-stu-id="943c3-149">MDB</span></span>     |<span data-ttu-id="943c3-150">ESENT (výchozí), MDB</span><span class="sxs-lookup"><span data-stu-id="943c3-150">ESENT (Default), MDB</span></span> |<span data-ttu-id="943c3-151">ESENT (výchozí), MDB</span><span class="sxs-lookup"><span data-stu-id="943c3-151">ESENT (Default), MDB</span></span>|<span data-ttu-id="943c3-152">ESENT (výchozí), SQL Server, MDB</span><span class="sxs-lookup"><span data-stu-id="943c3-152">ESENT (Default), SQL Server, MDB</span></span>

<span data-ttu-id="943c3-153">Od verze 17090 z [Insider Preview systému Windows Server](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server je podporovaná možnost pro službu o přijetí změn (funkce Windows *DSC služby*).</span><span class="sxs-lookup"><span data-stu-id="943c3-153">Starting in release 17090 of [Windows Server Insider Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server is a supported option for the Pull Service (Windows Feature *DSC-Service*).</span></span>  <span data-ttu-id="943c3-154">To poskytne nové možnosti pro škálování velkých prostředích DSC, které jste nemigrovali do [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span><span class="sxs-lookup"><span data-stu-id="943c3-154">This provides a new option for scaling large DSC environments that have not migrated to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span></span>

> <span data-ttu-id="943c3-155">**Poznámka:**: Podpora systému SQL Server nebude přidán do předchozí verze WMF 5.1 (nebo starší) a budou k dispozici na Windows Server verze větší než nebo rovna hodnotě 17090 pouze.</span><span class="sxs-lookup"><span data-stu-id="943c3-155">**Note**: SQL Server support will not be added to previous versions of WMF 5.1 (or earlier) and will only be available on Windows Server versions greater than or equal to 17090.</span></span>

<span data-ttu-id="943c3-156">Chcete-li nakonfigurovat serveru vyžádané replikace používat SQL Server, nastavte **SqlProvider** k `$true` a **SqlConnectionString** na platný připojovací řetězec SQL serveru.</span><span class="sxs-lookup"><span data-stu-id="943c3-156">To configure the pull server to use SQL Server, set **SqlProvider** to `$true` and **SqlConnectionString** to a valid SQL Server Connection String.</span></span>  <span data-ttu-id="943c3-157">Další informace najdete v tématu [SqlClient připojovací řetězce](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).</span><span class="sxs-lookup"><span data-stu-id="943c3-157">For more information, see [SqlClient Connection Strings](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).</span></span>
<span data-ttu-id="943c3-158">Příklad konfigurace SQL serveru s **xDscWebService**, nejdřív přečíst [pomocí prostředků xDscWebService](#using-the-xdscwebservice-resource) a pak si projděte [Sample_xDscWebServiceRegistration_ UseSQLProvider.ps1 na Githubu](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).</span><span class="sxs-lookup"><span data-stu-id="943c3-158">For an example of SQL Server configuration with **xDscWebService**, first read [Using the xDscWebService resource](#using-the-xdscwebservice-resource) and then review [Sample_xDscWebServiceRegistration_UseSQLProvider.ps1 on GitHub](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).</span></span>

### <a name="using-the-xdscwebservice-resource"></a><span data-ttu-id="943c3-159">Použití prostředků xDscWebService</span><span class="sxs-lookup"><span data-stu-id="943c3-159">Using the xDscWebService resource</span></span>

<span data-ttu-id="943c3-160">Nejjednodušší způsob, jak nastavit webového serveru vyžádané replikace je použít **xDscWebService** zdrojů, součástí **xPSDesiredStateConfiguration** modulu.</span><span class="sxs-lookup"><span data-stu-id="943c3-160">The easiest way to set up a web pull server is to use the **xDscWebService** resource, included in the **xPSDesiredStateConfiguration** module.</span></span>
<span data-ttu-id="943c3-161">Následující postup vysvětluje, jak použít zdroje v konfiguraci, který nastaví kolekci webové služby.</span><span class="sxs-lookup"><span data-stu-id="943c3-161">The following steps explain how to use the resource in a configuration that sets up the web service.</span></span>

1. <span data-ttu-id="943c3-162">Volání [Install-Module](/powershell/module/PowershellGet/Install-Module) rutinu instalace **xPSDesiredStateConfiguration** modulu.</span><span class="sxs-lookup"><span data-stu-id="943c3-162">Call the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to install the **xPSDesiredStateConfiguration** module.</span></span> <span data-ttu-id="943c3-163">**Poznámka:**: **Install-Module** je součástí **PowerShellGet** modulu, která je obsažena v Powershellu 5.0.</span><span class="sxs-lookup"><span data-stu-id="943c3-163">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="943c3-164">Můžete stáhnout **PowerShellGet** modulu pro PowerShell 3.0 a 4.0 na [Preview moduly Powershellu PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="943c3-164">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>
1. <span data-ttu-id="943c3-165">Získejte certifikát SSL pro server o přijetí změn DSC od důvěryhodné certifikační autority, buď v rámci vaší organizace nebo veřejné autority.</span><span class="sxs-lookup"><span data-stu-id="943c3-165">Get an SSL certificate for the DSC Pull server from a trusted Certificate Authority, either within your organization or a public authority.</span></span> <span data-ttu-id="943c3-166">Certifikát obdržený od autority se obvykle ve formátu PFX.</span><span class="sxs-lookup"><span data-stu-id="943c3-166">The certificate received from the authority is usually in the PFX format.</span></span> <span data-ttu-id="943c3-167">Nainstalujte certifikát na uzlu, který se stane serveru vyžádané replikace DSC ve výchozím umístění, které by se měly CERT: \LocalMachine\My.</span><span class="sxs-lookup"><span data-stu-id="943c3-167">Install the certificate on the node that will become the DSC Pull server in the default location, which should be CERT:\LocalMachine\My.</span></span> <span data-ttu-id="943c3-168">Poznamenejte si kryptografický otisk certifikátu.</span><span class="sxs-lookup"><span data-stu-id="943c3-168">Make a note of the certificate thumbprint.</span></span>
1. <span data-ttu-id="943c3-169">Vyberte identifikátor GUID, který se použije jako registrační klíč.</span><span class="sxs-lookup"><span data-stu-id="943c3-169">Select a GUID to be used as the Registration Key.</span></span> <span data-ttu-id="943c3-170">Chcete-li vygenerovat pomocí prostředí PowerShell zadejte na příkazovém řádku PS a stiskněte klávesu enter: "``` [guid]::newGuid()```'nebo'```New-Guid```".</span><span class="sxs-lookup"><span data-stu-id="943c3-170">To generate one using PowerShell enter the following at the PS prompt and press enter: '``` [guid]::newGuid()```' or '```New-Guid```'.</span></span> <span data-ttu-id="943c3-171">Tento klíč se použije klient uzly jako sdílený klíč k ověření během registrace.</span><span class="sxs-lookup"><span data-stu-id="943c3-171">This key will be used by client nodes as a shared key to authenticate during registration.</span></span> <span data-ttu-id="943c3-172">Další informace najdete v článku níže uvedené části registrační klíč.</span><span class="sxs-lookup"><span data-stu-id="943c3-172">For more information, see the Registration Key section below.</span></span>
1. <span data-ttu-id="943c3-173">V prostředí PowerShell ISE spustit (F5) následující konfigurační skript (zahrnutý ve složce Příklady **xPSDesiredStateConfiguration** modul jako Sample_xDscWebServiceRegistration.ps1).</span><span class="sxs-lookup"><span data-stu-id="943c3-173">In the PowerShell ISE, start (F5) the following configuration script (included in the Examples folder of the  **xPSDesiredStateConfiguration** module as Sample_xDscWebServiceRegistration.ps1).</span></span> <span data-ttu-id="943c3-174">Tento skript nastaví serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="943c3-174">This script sets up the pull server.</span></span>

    ```powershell
    configuration Sample_xDscWebServiceRegistration
    {
        param
        (
            [string[]]$NodeName = 'localhost',

            [ValidateNotNullOrEmpty()]
            [string] $certificateThumbPrint,

            [Parameter(HelpMessage='This should be a string with enough entropy (randomness) to protect the registration of clients to the pull server.  We will use new GUID by default.')]
            [ValidateNotNullOrEmpty()]
            [string] $RegistrationKey   # A guid that clients use to initiate conversation with pull server
        )

        Import-DSCResource -ModuleName xPSDesiredStateConfiguration

        Node $NodeName
        {
            WindowsFeature DSCServiceFeature
            {
                Ensure = "Present"
                Name   = "DSC-Service"
            }

            xDscWebService PSDSCPullServer
            {
                Ensure                  = "Present"
                EndpointName            = "PSDSCPullServer"
                Port                    = 8080
                PhysicalPath            = "$env:SystemDrive\inetpub\PSDSCPullServer"
                CertificateThumbPrint   = $certificateThumbPrint
                ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
                ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
                State                   = "Started"
                DependsOn               = "[WindowsFeature]DSCServiceFeature"
                RegistrationKeyPath     = "$env:PROGRAMFILES\WindowsPowerShell\DscService"
                AcceptSelfSignedCertificates = $true
                Enable32BitAppOnWin64   = $false
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

1. <span data-ttu-id="943c3-175">Spustit konfiguraci předávání kryptografický otisk certifikátu protokolu SSL, jako **certificateThumbPrint** parametr a identifikátor GUID registrační klíč jako **RegistrationKey** parametr:</span><span class="sxs-lookup"><span data-stu-id="943c3-175">Run the configuration, passing the thumbprint of the SSL certificate as the **certificateThumbPrint** parameter and a GUID registration key as the **RegistrationKey** parameter:</span></span>

    ```powershell
    # To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store
    # and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
    dir Cert:\LocalMachine\my

    # Then include this thumbprint when running the configuration
    Sample_xDscWebServiceRegistration -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

    # Run the compiled configuration to make the target node a DSC Pull Server
    Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
    ```

#### <a name="registration-key"></a><span data-ttu-id="943c3-176">Registrační klíč</span><span class="sxs-lookup"><span data-stu-id="943c3-176">Registration Key</span></span>

<span data-ttu-id="943c3-177">Povolit klientské uzly zaregistrovat serveru tak, aby se používají názvy konfigurace namísto ID konfigurace, registrační klíč, který byl vytvořen v konfiguraci uvedené výš se uloží do souboru s názvem `RegistrationKeys.txt` v `C:\Program Files\WindowsPowerShell\DscService`.</span><span class="sxs-lookup"><span data-stu-id="943c3-177">To allow client nodes to register with the server so that they can use configuration names instead of a configuration ID, a registration key that was created by the above configuration is saved in a file named `RegistrationKeys.txt` in `C:\Program Files\WindowsPowerShell\DscService`.</span></span> <span data-ttu-id="943c3-178">Registrační klíč funguje jako sdílený tajný klíč použít při počáteční registraci klienta se serverem pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="943c3-178">The registration key functions as a shared secret used during the initial registration by the client with the pull server.</span></span> <span data-ttu-id="943c3-179">Klient vygeneruje certifikát podepsaný svým držitelem, který slouží k jednoznačné ověření na serveru vyžádané replikace po úspěšném dokončení registrace.</span><span class="sxs-lookup"><span data-stu-id="943c3-179">The client will generate a self-signed certificate that is used to uniquely authenticate to the pull server once registration is successfully completed.</span></span> <span data-ttu-id="943c3-180">Kryptografický otisk tohoto certifikátu se ukládají místně a přidružené k adrese URL serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="943c3-180">The thumbprint of this certificate is stored locally and associated with the URL of the pull server.</span></span>
> <span data-ttu-id="943c3-181">**Poznámka:**: Registrace klíče nejsou podporovány v Powershellu 4.0.</span><span class="sxs-lookup"><span data-stu-id="943c3-181">**Note**: Registration keys are not supported in PowerShell 4.0.</span></span>

<span data-ttu-id="943c3-182">Aby bylo možné konfigurovat uzel k ověření na serveru vyžádané replikace, registrační klíč musí být v metaconfiguration pro libovolný cílový uzel, který se registruje k tomuto serveru o přijetí změn.</span><span class="sxs-lookup"><span data-stu-id="943c3-182">In order to configure a node to authenticate with the pull server, the registration key needs to be in the metaconfiguration for any target node that will be registering with this pull server.</span></span> <span data-ttu-id="943c3-183">Všimněte si, **RegistrationKey** ve níže metaconfiguration se odebere, až cílový počítač se úspěšně zaregistrovala, a hodnota "140a952b-b9d6-406b-b416-e0f759c9c0e4" musí odpovídat hodnotu uloženou v RegistrationKeys.txt soubor na serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="943c3-183">Note that the **RegistrationKey** in the metaconfiguration below is removed after the target machine has successfully registered, and that the value '140a952b-b9d6-406b-b416-e0f759c9c0e4' must match the value stored in the RegistrationKeys.txt file on the pull server.</span></span> <span data-ttu-id="943c3-184">Je vždy nutné považovat hodnotu klíče registrace bezpečné, protože mého vědomí jakékoli cílový počítač zaregistrovat u serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="943c3-184">Always treat the registration key value securely, because knowing it allows any target machine to register with the pull server.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration Sample_MetaConfigurationToRegisterWithLessSecurePullServer
{
    param
    (
        [ValidateNotNullOrEmpty()]
        [string] $NodeName = 'localhost',

        [ValidateNotNullOrEmpty()]
        [string] $RegistrationKey, #same as the one used to set up pull server in previous configuration

        [ValidateNotNullOrEmpty()]
        [string] $ServerName = 'localhost' #node name of the pull server, same as $NodeName used in previous configuration
    )

    Node $NodeName
    {
        Settings
        {
            RefreshMode        = 'Pull'
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL          = "https://$ServerName`:8080/PSDSCPullServer.svc" # notice it is https
            RegistrationKey    = $RegistrationKey
            ConfigurationNames = @('ClientConfig')
        }

        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL       = "https://$ServerName`:8080/PSDSCPullServer.svc" # notice it is https
            RegistrationKey = $RegistrationKey
        }
    }
}

Sample_MetaConfigurationToRegisterWithLessSecurePullServer -RegistrationKey $RegistrationKey -OutputPath c:\Configs\TargetNodes
```

> <span data-ttu-id="943c3-185">**Poznámka:**: **ReportServerWeb** část umožňuje vykazování dat k odeslání do serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="943c3-185">**Note**: The **ReportServerWeb** section allows reporting data to be sent to the pull server.</span></span>

<span data-ttu-id="943c3-186">Chybějící **ConfigurationID** vlastnost v souboru metaconfiguration implicitně znamená, že tohoto serveru vyžádané replikace se nepodporuje V2 verze serveru protokolu o přijetí změn, a proto počáteční registrace je povinný.</span><span class="sxs-lookup"><span data-stu-id="943c3-186">The lack of the **ConfigurationID** property in the metaconfiguration file implicitly means that pull server is supporting the V2 version of the pull server protocol so an initial registration is required.</span></span>
<span data-ttu-id="943c3-187">Naopak přítomnost **ConfigurationID** znamená, že je použita verze V1 serveru protokolu o přijetí změn a neexistuje žádné zpracování registrace.</span><span class="sxs-lookup"><span data-stu-id="943c3-187">Conversely, the presence of a **ConfigurationID** means that the V1 version of the pull server protocol is used and there is no registration processing.</span></span>

><span data-ttu-id="943c3-188">**Poznámka:**: Ve scénáři NABÍZENÝCH chybu existuje v aktuální verzi, díky které je potřeba definovat vlastnost ConfigurationID v souboru metaconfiguration uzlů, které jste nikdy zaregistrované serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="943c3-188">**Note**: In a PUSH scenario, a bug exists in the current release that makes it necessary to define a ConfigurationID property in the metaconfiguration file for nodes that have never registered with a pull server.</span></span> <span data-ttu-id="943c3-189">Se vynutí protokol serveru vyžádané replikace V1 a vyhněte se zprávy o selhání registrace.</span><span class="sxs-lookup"><span data-stu-id="943c3-189">This will force the V1 Pull Server protocol and avoid registration failure messages.</span></span>

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="943c3-190">Uvedení konfigurací a prostředků</span><span class="sxs-lookup"><span data-stu-id="943c3-190">Placing configurations and resources</span></span>

<span data-ttu-id="943c3-191">Za operace přijetí změn server dokončení instalačního programu, určené složky **ConfigurationPath** a **ModulePath** vlastnosti v konfiguraci serveru o přijetí změn jsou, kam umístíte modulů a konfigurací který bude k dispozici pro cílové uzly na vyžádání.</span><span class="sxs-lookup"><span data-stu-id="943c3-191">After the pull server setup completes, the folders defined by the **ConfigurationPath** and **ModulePath** properties in the pull server configuration are where you will place modules and configurations that will be available for target nodes to pull.</span></span>
<span data-ttu-id="943c3-192">Tyto soubory musí být v určitém formátu mohl serveru vyžádané replikace správně jejich zpracování.</span><span class="sxs-lookup"><span data-stu-id="943c3-192">These files need to be in a specific format in order for the pull server to correctly process them.</span></span>

### <a name="dsc-resource-module-package-format"></a><span data-ttu-id="943c3-193">Formát balíčku modulu prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="943c3-193">DSC resource module package format</span></span>

<span data-ttu-id="943c3-194">Každý modul prostředků musí být metoda ZIP a s názvem podle následujícího vzoru `{Module Name}_{Module Version}.zip`.</span><span class="sxs-lookup"><span data-stu-id="943c3-194">Each resource module needs to be zipped and named according to the following pattern `{Module Name}_{Module Version}.zip`.</span></span>
<span data-ttu-id="943c3-195">Například modul s názvem xWebAdminstration s verzí modulu 3.1.2.0 by se pojmenoval "xWebAdministration_3.2.1.0.zip".</span><span class="sxs-lookup"><span data-stu-id="943c3-195">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named 'xWebAdministration_3.2.1.0.zip'.</span></span>
<span data-ttu-id="943c3-196">Každá verze modulu musí být součástí jedné zip soubor.</span><span class="sxs-lookup"><span data-stu-id="943c3-196">Each version of a module must be contained in a single zip file.</span></span>
<span data-ttu-id="943c3-197">Vzhledem k tomu, že existuje pouze jedna verze prostředku v každém souboru zip, formát modulu přidáno ve WMF 5.0 díky podpoře pro více verzí modulu v jednom adresáři není podporován.</span><span class="sxs-lookup"><span data-stu-id="943c3-197">Since there is only a single version of a resource in each zip file, the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span>
<span data-ttu-id="943c3-198">To znamená, že před zabalení moduly prostředků DSC pro použití se serverem o přijetí změn budete muset proveďte malou změnu do struktury adresářů.</span><span class="sxs-lookup"><span data-stu-id="943c3-198">This means that before packaging up DSC resource modules for use with pull server you will need to make a small change to the directory structure.</span></span>
<span data-ttu-id="943c3-199">Výchozí formát pro moduly obsahující prostředek DSC ve WMF 5.0 je "{složku modulu}\{verze modulu} \DscResources\{Složka prostředků DSC}\'.</span><span class="sxs-lookup"><span data-stu-id="943c3-199">The default format of modules containing DSC resource in WMF 5.0 is '{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\'.</span></span>
<span data-ttu-id="943c3-200">Před balení do serveru vyžádané replikace, odeberte **{verze modulu}** složky, stane se cesta "{složku modulu} \DscResources\{Složka prostředků DSC}\'.</span><span class="sxs-lookup"><span data-stu-id="943c3-200">Before packaging up for the pull server, remove the **{Module version}** folder so the path becomes '{Module Folder}\DscResources\{DSC Resource Folder}\'.</span></span>
<span data-ttu-id="943c3-201">Díky této změně zip složce, jak je popsáno výše a umístí tyto souboru zip v **ModulePath** složky.</span><span class="sxs-lookup"><span data-stu-id="943c3-201">With this change, zip the folder as described above and place these zip files in the **ModulePath** folder.</span></span>

<span data-ttu-id="943c3-202">Použití `New-DscChecksum {module zip file}` vytvoření kontrolního součtu souboru pro nově přidaném modulu.</span><span class="sxs-lookup"><span data-stu-id="943c3-202">Use `New-DscChecksum {module zip file}` to create a checksum file for the newly added module.</span></span>

### <a name="configuration-mof-format"></a><span data-ttu-id="943c3-203">Formát MOF konfigurace</span><span class="sxs-lookup"><span data-stu-id="943c3-203">Configuration MOF format</span></span>

<span data-ttu-id="943c3-204">Konfiguračního souboru MOF musí být párována s typem kontrolního součtu souboru tak, aby LCM na cílový uzel můžete konfiguraci ověřit.</span><span class="sxs-lookup"><span data-stu-id="943c3-204">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span>
<span data-ttu-id="943c3-205">Chcete-li vytvořit kontrolní součet, zavolejte [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) rutiny.</span><span class="sxs-lookup"><span data-stu-id="943c3-205">To create a checksum, call the [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) cmdlet.</span></span>
<span data-ttu-id="943c3-206">Přijímá rutina **cesta** parametr, který určuje složku, ve kterém se nachází konfigurační soubor MOF.</span><span class="sxs-lookup"><span data-stu-id="943c3-206">The cmdlet takes a **Path** parameter that specifies the folder where the configuration MOF is located.</span></span>
<span data-ttu-id="943c3-207">Rutina vytvoří kontrolní součet souboru s názvem `ConfigurationMOFName.mof.checksum`, kde `ConfigurationMOFName` je název konfiguračního souboru mof.</span><span class="sxs-lookup"><span data-stu-id="943c3-207">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span>
<span data-ttu-id="943c3-208">Pokud existuje více než jednu konfiguraci soubory MOF v zadané složce, kontrolní součet se vytvoří pro každou konfiguraci ve složce.</span><span class="sxs-lookup"><span data-stu-id="943c3-208">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span>
<span data-ttu-id="943c3-209">Umístěte soubory MOF a jejich přidružené kontrolního součtu souborů v **ConfigurationPath** složky.</span><span class="sxs-lookup"><span data-stu-id="943c3-209">Place the MOF files and their associated checksum files in the **ConfigurationPath** folder.</span></span>

><span data-ttu-id="943c3-210">**Poznámka:**: Pokud změníte konfiguračního souboru MOF žádným způsobem, je nutné znovu vytvořit kontrolní součet souboru.</span><span class="sxs-lookup"><span data-stu-id="943c3-210">**Note**: If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

### <a name="tooling"></a><span data-ttu-id="943c3-211">Nástroje</span><span class="sxs-lookup"><span data-stu-id="943c3-211">Tooling</span></span>

<span data-ttu-id="943c3-212">Aby bylo možné tvoří nastavení, ověřování a správě serveru vyžádané replikace jednodušší, tyto nástroje jsou zahrnuty jako příklady v nejnovější verzi modulu xPSDesiredStateConfiguration:</span><span class="sxs-lookup"><span data-stu-id="943c3-212">In order to make setting up, validating and managing the pull server easier, the following tools are included as examples in the latest version of the xPSDesiredStateConfiguration module:</span></span>

1. <span data-ttu-id="943c3-213">Modul, který vám pomůže s balení moduly prostředků DSC a konfigurační soubory pro použití na serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="943c3-213">A module that will help with packaging DSC resource modules and configuration files for use on the pull server.</span></span> <span data-ttu-id="943c3-214">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span><span class="sxs-lookup"><span data-stu-id="943c3-214">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span></span> <span data-ttu-id="943c3-215">Následující příklady:</span><span class="sxs-lookup"><span data-stu-id="943c3-215">Examples below:</span></span>

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @('xWebAdministration', 'xPhp')
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. <span data-ttu-id="943c3-216">Skript, který se ověřuje serveru vyžádané replikace je správně nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="943c3-216">A script that validates the pull server is configured correctly.</span></span> <span data-ttu-id="943c3-217">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span><span class="sxs-lookup"><span data-stu-id="943c3-217">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span></span>

## <a name="community-solutions-for-pull-service"></a><span data-ttu-id="943c3-218">Řešení komunity pro službu přijetí změn</span><span class="sxs-lookup"><span data-stu-id="943c3-218">Community Solutions for Pull Service</span></span>

<span data-ttu-id="943c3-219">Společenství DSC autorem více řešení, která implementují protokol služby o přijetí změn.</span><span class="sxs-lookup"><span data-stu-id="943c3-219">The DSC community has authored multiple solutions to implement the pull service protocol.</span></span>
<span data-ttu-id="943c3-220">Pro místní prostředí nabízejí schopnosti služeb o přijetí změn a možnost zpětně přispívat ke komunitě přírůstková vylepšení.</span><span class="sxs-lookup"><span data-stu-id="943c3-220">For on-premises environments, these offer pull service capabilities and an opportunity to contribute back to the community with incremental enhancements.</span></span>

- [<span data-ttu-id="943c3-221">Tug</span><span class="sxs-lookup"><span data-stu-id="943c3-221">Tug</span></span>](https://github.com/powershellorg/tug)
- [<span data-ttu-id="943c3-222">DSC TRÆK</span><span class="sxs-lookup"><span data-stu-id="943c3-222">DSC-TRÆK</span></span>](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a><span data-ttu-id="943c3-223">Konfigurace klienta o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="943c3-223">Pull client configuration</span></span>

<span data-ttu-id="943c3-224">Toto téma popisuje nastavení klientů o přijetí změn podrobně:</span><span class="sxs-lookup"><span data-stu-id="943c3-224">The following topics describe setting up pull clients in detail:</span></span>

- [<span data-ttu-id="943c3-225">Nastavení načítacího klienta DSC použití konfiguračních identifikátorů</span><span class="sxs-lookup"><span data-stu-id="943c3-225">Set up a DSC pull client using a configuration ID</span></span>](pullClientConfigID.md)
- [<span data-ttu-id="943c3-226">Nastavení načítacího klienta DSC použití konfiguračních názvů</span><span class="sxs-lookup"><span data-stu-id="943c3-226">Set up a DSC pull client using configuration names</span></span>](pullClientConfigNames.md)
- [<span data-ttu-id="943c3-227">Částečné konfigurace</span><span class="sxs-lookup"><span data-stu-id="943c3-227">Partial configurations</span></span>](partialConfigs.md)

## <a name="see-also"></a><span data-ttu-id="943c3-228">Viz taky</span><span class="sxs-lookup"><span data-stu-id="943c3-228">See also</span></span>

- [<span data-ttu-id="943c3-229">Prostředí Windows PowerShell Desired State Configuration – přehled</span><span class="sxs-lookup"><span data-stu-id="943c3-229">Windows PowerShell Desired State Configuration Overview</span></span>](../overview/overview.md)
- [<span data-ttu-id="943c3-230">Přijetí konfigurace</span><span class="sxs-lookup"><span data-stu-id="943c3-230">Enacting configurations</span></span>](enactingConfigurations.md)
- [<span data-ttu-id="943c3-231">Použití serveru sestav DSC</span><span class="sxs-lookup"><span data-stu-id="943c3-231">Using a DSC report server</span></span>](reportServer.md)
- <span data-ttu-id="943c3-232">[[MS-DSCPM]: Desired State Configuration protokol modelu o přijetí změn](https://msdn.microsoft.com/library/dn393548.aspx)</span><span class="sxs-lookup"><span data-stu-id="943c3-232">[[MS-DSCPM]: Desired State Configuration Pull Model Protocol](https://msdn.microsoft.com/library/dn393548.aspx)</span></span>
- <span data-ttu-id="943c3-233">[[MS-DSCPM]: Desired State Configuration chyby protokolu modelu o přijetí změn](https://msdn.microsoft.com/library/mt612824.aspx)</span><span class="sxs-lookup"><span data-stu-id="943c3-233">[[MS-DSCPM]: Desired State Configuration Pull Model Protocol Errata](https://msdn.microsoft.com/library/mt612824.aspx)</span></span>
